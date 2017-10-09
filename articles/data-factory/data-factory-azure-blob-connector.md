---
title: aaaCopy dati in o dall'archiviazione Blob di Azure | Documenti Microsoft
description: 'Informazioni su come toocopy blob di dati in Azure Data Factory. Usare questo esempio: come toocopy tooand di dati dall''archiviazione Blob di Azure e Database SQL di Azure.'
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
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="39ba8-105">Copia dati tooor dall'archiviazione Blob di Azure usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="39ba8-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="39ba8-106">Questo articolo spiega come toouse hello attività di copia in Azure Data Factory toocopy dati tooand dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="39ba8-107">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="39ba8-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="39ba8-108">Overview</span></span>
<span data-ttu-id="39ba8-109">È possibile copiare dati da qualsiasi origine supportati dati tooAzure nell'archiviazione Blob di archiviazione o da dati di archiviazione Blob di Azure supportata tooany sink archivio.</span><span class="sxs-lookup"><span data-stu-id="39ba8-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="39ba8-110">Hello nella tabella seguente fornisce un elenco di archivi dati supportata come origini o sink dall'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="39ba8-111">È ad esempio possibile spostare dati **da** un database di SQL Server o un database SQL di Azure **a** una risorsa di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="39ba8-112">È anche possibile copiare dati **da** Archiviazione BLOB di Azure **a** un'istanza di Azure SQL Data Warehouse o una raccolta Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="39ba8-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="39ba8-113">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="39ba8-113">Supported scenarios</span></span>
<span data-ttu-id="39ba8-114">È possibile copiare dati **dall'archiviazione Blob di Azure** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="39ba8-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="39ba8-115">È possibile copiare dati da archivi dati seguenti hello **tooAzure nell'archiviazione Blob**:</span><span class="sxs-lookup"><span data-stu-id="39ba8-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="39ba8-116">Supporta la copia dei dati da attività di copia / tooboth account generici di archiviazione di Azure e a caldo/raffreddare nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="39ba8-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="39ba8-117">supporta attività Hello **letto dal blocco, Accodamento o BLOB di pagine**, ma supporta **scrittura BLOB in blocchi tooonly**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="39ba8-118">Archiviazione Premium di Azure non è supportata come sink poiché si basa sui BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="39ba8-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="39ba8-119">Attività di copia non elimina dati dall'origine hello dopo hello dati vengono correttamente copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="39ba8-120">Se sono necessari dati di origine toodelete dopo una copia ha esito positivo, creare un [attività personalizzata](data-factory-use-custom-activities.md) toodelete hello dati e utilizzare attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="39ba8-121">Per un esempio, vedere hello [esempio blob o una cartella di eliminazione in GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="39ba8-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="39ba8-122">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="39ba8-122">Get started</span></span>
<span data-ttu-id="39ba8-123">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un archivio BLOB di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="39ba8-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="39ba8-124">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="39ba8-125">In questo articolo ha un [procedura dettagliata](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) per la creazione di una pipeline toocopy dati da un tooanother di percorso di archiviazione Blob di Azure il percorso di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="39ba8-126">Per un'esercitazione sulla creazione di una pipeline toocopy dati da un Database SQL di tooAzure di archiviazione Blob di Azure, vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="39ba8-127">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="39ba8-128">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="39ba8-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="39ba8-129">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="39ba8-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="39ba8-130">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-130">Create a **data factory**.</span></span> <span data-ttu-id="39ba8-131">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="39ba8-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="39ba8-132">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="39ba8-133">Ad esempio, se si copiano dati da un database di SQL Azure tooan di archiviazione blob di Azure, è creare due servizi collegati toolink l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="39ba8-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="39ba8-134">Per le proprietà di servizio collegato che sono tooAzure specifico nell'archiviazione Blob, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="39ba8-135">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="39ba8-136">Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="39ba8-137">E, alla creazione di un altro set di dati toospecify hello SQL nella tabella nel database di SQL Azure hello che contiene dati hello copiati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="39ba8-138">Per le proprietà di set di dati che sono tooAzure specifico nell'archiviazione Blob, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="39ba8-139">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="39ba8-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="39ba8-140">Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e di SqlSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="39ba8-141">Analogamente, se si sta copiando tooAzure Database SQL di Azure nell'archiviazione Blob, utilizzare SqlSource e BlobSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="39ba8-142">Per le proprietà di attività di copia che sono tooAzure specifico nell'archiviazione Blob, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="39ba8-143">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="39ba8-144">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="39ba8-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="39ba8-145">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="39ba8-146">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un archivio Blob di Azure, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="39ba8-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="39ba8-147">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="39ba8-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="39ba8-148">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="39ba8-148">Linked service properties</span></span>
<span data-ttu-id="39ba8-149">Esistono due tipi di servizi collegati è possibile utilizzare toolink un servizio di archiviazione Azure tooan data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="39ba8-150">I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="39ba8-151">Hello servizio collegato di archiviazione di Azure fornisce data factory di hello con accesso globale toohello di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="39ba8-152">Mentre, hello Azure archiviazione SAS (firma di accesso condiviso) collegati servizio fornisce data factory di hello con accesso limitato/scadenza toohello di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="39ba8-153">Non esistono altre differenze tra questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="39ba8-154">Scegliere servizio hello collegato alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="39ba8-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="39ba8-155">Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="39ba8-156">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="39ba8-156">Dataset properties</span></span>
<span data-ttu-id="39ba8-157">toospecify toorepresent un set di dati dati di input o outpui in un archivio Blob di Azure, impostare proprietà di tipo hello del set di dati hello: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="39ba8-158">Set hello **linkedServiceName** servizio collegato di proprietà del nome di toohello hello set di dati di hello SAS di archiviazione di Azure o di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="39ba8-159">proprietà del tipo di set di dati hello Hello specificare hello **contenitore blob** hello e **cartella** nell'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="39ba8-160">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni di JSON, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="39ba8-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="39ba8-161">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="39ba8-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="39ba8-162">Data factory di supporta hello seguente i valori di tipo basata su .NET conformi a CLS per fornire informazioni sul tipo di "struttura" per le origini dati in lettura-schema come blob di Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="39ba8-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="39ba8-163">Data Factory esegue automaticamente le conversioni di tipo quando si spostano dati da un'origine tooa archiviano dati sink.</span><span class="sxs-lookup"><span data-stu-id="39ba8-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="39ba8-164">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e vengono fornite informazioni sulla posizione di hello, formattare e così via, dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="39ba8-165">sezione Hello typeProperties per set di dati di tipo **AzureBlob** set di dati è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="39ba8-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="39ba8-166">Proprietà</span><span class="sxs-lookup"><span data-stu-id="39ba8-166">Property</span></span> | <span data-ttu-id="39ba8-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="39ba8-167">Description</span></span> | <span data-ttu-id="39ba8-168">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="39ba8-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39ba8-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="39ba8-169">folderPath</span></span> |<span data-ttu-id="39ba8-170">Percorso toohello contenitore e della cartella nell'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="39ba8-171">Esempio: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="39ba8-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="39ba8-172">Sì</span><span class="sxs-lookup"><span data-stu-id="39ba8-172">Yes</span></span> |
| <span data-ttu-id="39ba8-173">fileName</span><span class="sxs-lookup"><span data-stu-id="39ba8-173">fileName</span></span> |<span data-ttu-id="39ba8-174">Nome del blob hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-174">Name of hello blob.</span></span> <span data-ttu-id="39ba8-175">fileName è facoltativo e non applica la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="39ba8-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="39ba8-176">Se si specifica un nome di file, hello attività (incluso copia) funziona su hello Blob specifico.</span><span class="sxs-lookup"><span data-stu-id="39ba8-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="39ba8-177">Quando non è stato specificato il nome del file, copia include tutti i BLOB in folderPath hello per input set di dati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="39ba8-178">Quando **fileName** non viene specificato per un set di dati di output e **preserveHierarchy** non è specificato nel sink di attività, hello nome del file hello generato potrebbe essere in hello segue questo formato: dati.<Guid>. txt (ad esempio:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="39ba8-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="39ba8-179">No</span><span class="sxs-lookup"><span data-stu-id="39ba8-179">No</span></span> |
| <span data-ttu-id="39ba8-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="39ba8-180">partitionedBy</span></span> |<span data-ttu-id="39ba8-181">partitionedBy è una proprietà facoltativa.</span><span class="sxs-lookup"><span data-stu-id="39ba8-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="39ba8-182">È possibile utilizzare è toospecify un dinamica folderPath e filename per dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="39ba8-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="39ba8-183">Ad esempio, è possibile includere parametri per ogni ora di dati in folderPath.</span><span class="sxs-lookup"><span data-stu-id="39ba8-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="39ba8-184">Vedere hello [utilizzando sezione proprietà partitionedBy](#using-partitionedBy-property) per informazioni dettagliate ed esempi.</span><span class="sxs-lookup"><span data-stu-id="39ba8-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="39ba8-185">No</span><span class="sxs-lookup"><span data-stu-id="39ba8-185">No</span></span> |
| <span data-ttu-id="39ba8-186">format</span><span class="sxs-lookup"><span data-stu-id="39ba8-186">format</span></span> | <span data-ttu-id="39ba8-187">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="39ba8-188">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="39ba8-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="39ba8-189">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="39ba8-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="39ba8-190">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="39ba8-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="39ba8-191">No</span><span class="sxs-lookup"><span data-stu-id="39ba8-191">No</span></span> |
| <span data-ttu-id="39ba8-192">compressione</span><span class="sxs-lookup"><span data-stu-id="39ba8-192">compression</span></span> | <span data-ttu-id="39ba8-193">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="39ba8-194">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="39ba8-195">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="39ba8-196">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="39ba8-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="39ba8-197">No</span><span class="sxs-lookup"><span data-stu-id="39ba8-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="39ba8-198">Uso della proprietà partitionedBy</span><span class="sxs-lookup"><span data-stu-id="39ba8-198">Using partitionedBy property</span></span>
<span data-ttu-id="39ba8-199">Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamico e il nome di dati della serie temporale con hello **partitionedBy** proprietà [funzioni di Data Factory e le variabili di sistema hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="39ba8-200">Per maggiori informazioni sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, leggere gli articoli [Creazione di set di dati](data-factory-create-datasets.md) e [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="39ba8-201">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="39ba8-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="39ba8-202">In questo esempio, {Slice} viene sostituito con valore hello della variabile di sistema di Data Factory SliceStart nel formato hello (YYYYMMDDHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="39ba8-203">Hello SliceStart fa riferimento l'ora toostart sezione hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="39ba8-204">Hello folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="39ba8-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="39ba8-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="39ba8-206">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="39ba8-206">Sample 2</span></span>

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

<span data-ttu-id="39ba8-207">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="39ba8-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="39ba8-208">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="39ba8-208">Copy activity properties</span></span>
<span data-ttu-id="39ba8-209">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="39ba8-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="39ba8-210">Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="39ba8-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="39ba8-211">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="39ba8-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="39ba8-212">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="39ba8-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="39ba8-213">Se si spostano dati da un archivio Blob di Azure, impostare il tipo di origine di hello nell'attività di copia hello troppo**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="39ba8-214">Analogamente, se si stanno spostando i dati tooan archiviazione Blob di Azure, impostare il tipo di sink hello nell'attività di copia hello troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="39ba8-215">Questa sezione presenta un elenco delle proprietà supportate da BlobSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="39ba8-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="39ba8-216">**BlobSource** supporta hello seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="39ba8-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="39ba8-217">Proprietà</span><span class="sxs-lookup"><span data-stu-id="39ba8-217">Property</span></span> | <span data-ttu-id="39ba8-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="39ba8-218">Description</span></span> | <span data-ttu-id="39ba8-219">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="39ba8-219">Allowed values</span></span> | <span data-ttu-id="39ba8-220">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="39ba8-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39ba8-221">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="39ba8-221">recursive</span></span> |<span data-ttu-id="39ba8-222">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="39ba8-223">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="39ba8-223">True (default value), False</span></span> |<span data-ttu-id="39ba8-224">No</span><span class="sxs-lookup"><span data-stu-id="39ba8-224">No</span></span> |

<span data-ttu-id="39ba8-225">**BlobSink** supporta le proprietà seguenti hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="39ba8-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="39ba8-226">Proprietà</span><span class="sxs-lookup"><span data-stu-id="39ba8-226">Property</span></span> | <span data-ttu-id="39ba8-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="39ba8-227">Description</span></span> | <span data-ttu-id="39ba8-228">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="39ba8-228">Allowed values</span></span> | <span data-ttu-id="39ba8-229">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="39ba8-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39ba8-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="39ba8-230">copyBehavior</span></span> |<span data-ttu-id="39ba8-231">Definisce il comportamento di copia hello quando origine hello è BlobSource o file System.</span><span class="sxs-lookup"><span data-stu-id="39ba8-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="39ba8-232"><b>PreserveHierarchy</b>: mantiene hello gerarchia del file nella cartella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="39ba8-233">percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="39ba8-234"><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello presenti hello primo livelli della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="39ba8-235">i file di destinazione Hello hanno nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="39ba8-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="39ba8-236"><b>Oggetto</b>: unisce tutti i file dal file tooone cartella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="39ba8-237">Se viene specificato il nome di File/Blob hello, il nome di file sottoposto a merge hello sarebbe nome specificato hello. in caso contrario, potrebbe essere il nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="39ba8-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="39ba8-238">No</span><span class="sxs-lookup"><span data-stu-id="39ba8-238">No</span></span> |

<span data-ttu-id="39ba8-239">**BlobSource** supporta anche le due proprietà seguenti per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="39ba8-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="39ba8-240">**treatEmptyAsNull**: Specifica se tootreat una stringa vuota o null come valore null.</span><span class="sxs-lookup"><span data-stu-id="39ba8-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="39ba8-241">**skipHeaderLineCount** : specifica il numero di righe che devono essere ignorate.</span><span class="sxs-lookup"><span data-stu-id="39ba8-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="39ba8-242">È applicabile solo quando il set di dati di input usa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="39ba8-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="39ba8-243">Analogamente, **BlobSink** supporta hello seguenti proprietà per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="39ba8-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="39ba8-244">**blobWriterAddHeader**: Specifica se un'intestazione di definizioni di colonna durante la scrittura tooan tooadd set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="39ba8-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="39ba8-245">Stessa funzionalità di hello hello supporto ora di set di dati seguenti proprietà che implementano: **treatEmptyAsNull**, **skipLineCount**, **prima riga come intestazione**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="39ba8-246">Hello nella tabella seguente fornisce informazioni aggiuntive sull'utilizzo delle proprietà dei set di dati al posto di queste proprietà di origine/sink blob nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="39ba8-247">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="39ba8-247">Copy Activity property</span></span> | <span data-ttu-id="39ba8-248">Proprietà del set di dati</span><span class="sxs-lookup"><span data-stu-id="39ba8-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="39ba8-249">skipHeaderLineCount in BlobSource</span><span class="sxs-lookup"><span data-stu-id="39ba8-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="39ba8-250">skipLineCount e firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="39ba8-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="39ba8-251">Le righe vengono ignorate prima e quindi di lettura di hello prima della riga come intestazione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="39ba8-252">treatEmptyAsNull in BlobSource</span><span class="sxs-lookup"><span data-stu-id="39ba8-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="39ba8-253">treatEmptyAsNull nel set di dati di input</span><span class="sxs-lookup"><span data-stu-id="39ba8-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="39ba8-254">blobWriterAddHeader in BlobSink</span><span class="sxs-lookup"><span data-stu-id="39ba8-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="39ba8-255">firstRowAsHeader nel set di dati di output</span><span class="sxs-lookup"><span data-stu-id="39ba8-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="39ba8-256">Per informazioni dettagliate su queste proprietà, vedere la sezione [Specifica di TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) .</span><span class="sxs-lookup"><span data-stu-id="39ba8-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="39ba8-257">esempi ricorsivi e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="39ba8-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="39ba8-258">In questa sezione viene descritto il comportamento risultante hello dell'operazione di copia hello per diverse combinazioni di valori ricorsiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="39ba8-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="39ba8-259">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="39ba8-259">recursive</span></span> | <span data-ttu-id="39ba8-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="39ba8-260">copyBehavior</span></span> | <span data-ttu-id="39ba8-261">Comportamento risultante</span><span class="sxs-lookup"><span data-stu-id="39ba8-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39ba8-262">true</span><span class="sxs-lookup"><span data-stu-id="39ba8-262">true</span></span> |<span data-ttu-id="39ba8-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="39ba8-263">preserveHierarchy</span></span> |<span data-ttu-id="39ba8-264">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="39ba8-265">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-265">Folder1</span></span><br/><span data-ttu-id="39ba8-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-268">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="39ba8-272">cartella di destinazione Hello Cartella1 viene creata con hello stessa struttura come origine di hello</span><span class="sxs-lookup"><span data-stu-id="39ba8-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="39ba8-273">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-273">Folder1</span></span><br/><span data-ttu-id="39ba8-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-276">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="39ba8-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="39ba8-280">true</span><span class="sxs-lookup"><span data-stu-id="39ba8-280">true</span></span> |<span data-ttu-id="39ba8-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="39ba8-281">flattenHierarchy</span></span> |<span data-ttu-id="39ba8-282">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="39ba8-283">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-283">Folder1</span></span><br/><span data-ttu-id="39ba8-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-286">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="39ba8-290">destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="39ba8-291">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-291">Folder1</span></span><br/><span data-ttu-id="39ba8-292">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="39ba8-293">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="39ba8-294">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="39ba8-295">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="39ba8-296">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="39ba8-297">true</span><span class="sxs-lookup"><span data-stu-id="39ba8-297">true</span></span> |<span data-ttu-id="39ba8-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="39ba8-298">mergeFiles</span></span> |<span data-ttu-id="39ba8-299">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="39ba8-300">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-300">Folder1</span></span><br/><span data-ttu-id="39ba8-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-303">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="39ba8-307">destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="39ba8-308">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-308">Folder1</span></span><br/><span data-ttu-id="39ba8-309">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome file generato automaticamente</span><span class="sxs-lookup"><span data-stu-id="39ba8-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="39ba8-310">false</span><span class="sxs-lookup"><span data-stu-id="39ba8-310">false</span></span> |<span data-ttu-id="39ba8-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="39ba8-311">preserveHierarchy</span></span> |<span data-ttu-id="39ba8-312">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="39ba8-313">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-313">Folder1</span></span><br/><span data-ttu-id="39ba8-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-316">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="39ba8-320">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura</span><span class="sxs-lookup"><span data-stu-id="39ba8-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="39ba8-321">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-321">Folder1</span></span><br/><span data-ttu-id="39ba8-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="39ba8-324">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="39ba8-325">false</span><span class="sxs-lookup"><span data-stu-id="39ba8-325">false</span></span> |<span data-ttu-id="39ba8-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="39ba8-326">flattenHierarchy</span></span> |<span data-ttu-id="39ba8-327">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="39ba8-328">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-328">Folder1</span></span><br/><span data-ttu-id="39ba8-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-331">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="39ba8-335">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura</span><span class="sxs-lookup"><span data-stu-id="39ba8-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="39ba8-336">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-336">Folder1</span></span><br/><span data-ttu-id="39ba8-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="39ba8-338">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="39ba8-339">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="39ba8-340">false</span><span class="sxs-lookup"><span data-stu-id="39ba8-340">false</span></span> |<span data-ttu-id="39ba8-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="39ba8-341">mergeFiles</span></span> |<span data-ttu-id="39ba8-342">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="39ba8-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="39ba8-343">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-343">Folder1</span></span><br/><span data-ttu-id="39ba8-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="39ba8-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="39ba8-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="39ba8-346">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="39ba8-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="39ba8-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="39ba8-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="39ba8-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="39ba8-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="39ba8-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="39ba8-350">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura</span><span class="sxs-lookup"><span data-stu-id="39ba8-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="39ba8-351">Cartella1</span><span class="sxs-lookup"><span data-stu-id="39ba8-351">Folder1</span></span><br/><span data-ttu-id="39ba8-352">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="39ba8-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="39ba8-353">Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="39ba8-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="39ba8-354">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="39ba8-355">Procedura dettagliata: Utilizzare Copia guidata toocopy dati da e verso l'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="39ba8-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="39ba8-356">Esaminare la modalità di archiviazione blob tooquickly copia dati da e verso un Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="39ba8-357">In questa procedura dettagliata gli archivi dati sia di origine che di destinazione sono di tipo archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="39ba8-358">Hello pipeline in questa procedura dettagliata consente di copiare dati da una cartella tooanother cartella hello stesso contenitore di blob.</span><span class="sxs-lookup"><span data-stu-id="39ba8-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="39ba8-359">Questa procedura dettagliata è intenzionalmente semplice tooshow impostazioni o proprietà quando si utilizza l'archiviazione Blob come origine o sink.</span><span class="sxs-lookup"><span data-stu-id="39ba8-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="39ba8-360">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="39ba8-360">Prerequisites</span></span>
1. <span data-ttu-id="39ba8-361">Creare un **account di archiviazione di Azure** per utilizzo generico, se necessario.</span><span class="sxs-lookup"><span data-stu-id="39ba8-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="39ba8-362">Usare l'archiviazione blob hello sia **origine** e **destinazione** archivio dati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="39ba8-363">Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo per passaggi toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="39ba8-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="39ba8-364">Creare un contenitore blob denominato **adfblobconnector** nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="39ba8-365">Creare una cartella denominata **input** in hello **adfblobconnector** contenitore.</span><span class="sxs-lookup"><span data-stu-id="39ba8-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="39ba8-366">Creare un file denominato **emp.txt** con hello dopo il contenuto e caricarla toohello **input** cartella tramite strumenti [Esplora archivi Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="39ba8-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="39ba8-367">Creare hello data factory</span><span class="sxs-lookup"><span data-stu-id="39ba8-367">Create hello data factory</span></span>
1. <span data-ttu-id="39ba8-368">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="39ba8-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="39ba8-369">Fare clic su **+ nuovo** dall'angolo superiore sinistro di hello, fare clic su **Intelligence + analitica**, fare clic su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="39ba8-370">In hello **nuova data factory** pannello:</span><span class="sxs-lookup"><span data-stu-id="39ba8-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="39ba8-371">Immettere **ADFBlobConnectorDF** per hello **nome**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="39ba8-372">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="39ba8-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="39ba8-373">Se viene visualizzato l'errore hello: `*Data factory name “ADFBlobConnectorDF” is not available`, modificare il nome di hello di hello data factory (ad esempio, yournameADFBlobConnectorDF) e provare a creare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="39ba8-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="39ba8-374">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="39ba8-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="39ba8-375">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="39ba8-376">Per il gruppo di risorse, selezionare **Usa esistente** tooselect un esistente risorsa gruppo (o) selezionare **Crea nuovo** tooenter un nome per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="39ba8-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="39ba8-377">Selezionare un **percorso** per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="39ba8-378">Selezionare **toodashboard Pin** casella di controllo nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="39ba8-379">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-379">Click **Create**.</span></span>
3. <span data-ttu-id="39ba8-380">Una volta completata la creazione di hello, vedrai hello **Data Factory** pannello, come illustrato nella seguente immagine hello: ![home page di Data factory](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="39ba8-381">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="39ba8-381">Copy Wizard</span></span>
1. <span data-ttu-id="39ba8-382">Nella home page di hello Data Factory, fare clic su hello **copia dei dati [anteprima]** riquadro toolaunch **copia dati guidata** in una scheda separata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="39ba8-383">Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", disabilitare o deselezionare **bloccare i cookie di terze parti e i dati del sito** (oppure) mantenere abilitato e creare un'eccezione per **login.microsoftonline.com**e quindi provare ad avviare la procedura guidata hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="39ba8-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="39ba8-384">In hello **proprietà** pagina:</span><span class="sxs-lookup"><span data-stu-id="39ba8-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="39ba8-385">Immettere **CopyPipeline** in **Nome attività**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="39ba8-386">Nome attività Hello è hello della pipeline hello nella data factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="39ba8-387">Immettere un **descrizione** per attività hello (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="39ba8-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="39ba8-388">Per **ritmo di attività o l'utilità di pianificazione**, mantenere hello **esecuzione a intervalli regolari su pianificazione** opzione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="39ba8-389">Se si desidera toorun questa attività una sola volta anziché eseguire ripetutamente una pianificazione, selezionare **Esegui una volta**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="39ba8-390">Se si seleziona l'opzione **Run once now** (Esegui una volta ora), viene creata una [pipeline con esecuzione singola](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="39ba8-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="39ba8-391">Mantenere le impostazioni di hello per **periodica modello**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="39ba8-392">Questa attività viene eseguito ogni giorno tra hello iniziare e termina volte è specificata al passaggio successivo di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="39ba8-393">Hello modifica **data ora di inizio** troppo**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="39ba8-394">Hello modifica **data e ora fine** troppo**25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="39ba8-395">È opportuno data hello tootype invece di dover passare attraverso il calendario hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="39ba8-396">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-396">Click **Next**.</span></span>
      <span data-ttu-id="39ba8-397">![Strumento di copia - Pagina Proprietà](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="39ba8-398">In hello **archivio dati di origine** pagina, fare clic su **archiviazione Blob di Azure** riquadro.</span><span class="sxs-lookup"><span data-stu-id="39ba8-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="39ba8-399">Usare l'archivio dati di origine di pagina toospecify hello per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="39ba8-400">È possibile usare un servizio collegato di archivio dati esistente oppure specificare un nuovo archivio dati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="39ba8-401">servizio collegato toouse esistente, selezionare **da servizi esistenti collegati** e selezionare hello destra servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="39ba8-402">![Strumento di copia - Pagina Archivio dati di origine](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="39ba8-403">In hello **specificare account di archiviazione Blob di Azure hello** pagina:</span><span class="sxs-lookup"><span data-stu-id="39ba8-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="39ba8-404">Nome generato automaticamente hello per mantenere **nome connessione**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="39ba8-405">nome della connessione Hello è il nome di hello del servizio di hello collegato di tipo: archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="39ba8-406">Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="39ba8-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="39ba8-407">Selezionare la sottoscrizione di Azure o mantenere **Seleziona tutte** per **Sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="39ba8-408">Selezionare un **account di archiviazione Azure** da hello account disponibile nella sottoscrizione selezionata hello l'elenco di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="39ba8-409">È anche possibile scegliere tooenter impostazioni dell'account di archiviazione manualmente selezionando **immettere manualmente** opzione per hello **metodo di selezione dell'Account**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="39ba8-410">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-410">Click **Next**.</span></span> 
      <span data-ttu-id="39ba8-411">![Strumento Copia: specificare l'account di archiviazione Blob di Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="39ba8-412">In **cartella o file di input hello scegliere** pagina:</span><span class="sxs-lookup"><span data-stu-id="39ba8-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="39ba8-413">Fare doppio clic su **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="39ba8-414">Selezionare **input** e fare clic su **Scegli**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="39ba8-415">In questa procedura dettagliata, si seleziona una cartella di input hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="39ba8-416">È anche possibile selezionare file emp.txt hello nella cartella hello invece.</span><span class="sxs-lookup"><span data-stu-id="39ba8-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="39ba8-417">![Strumento Copia - scegliere i file di input hello o cartella](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="39ba8-418">In hello **cartella o file di input hello scegliere** pagina:</span><span class="sxs-lookup"><span data-stu-id="39ba8-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="39ba8-419">Verificare che hello **file o cartella** è troppo**adfblobconnector/input**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="39ba8-420">Se il file hello si trovano in sottocartelle, ad esempio, 2017/04/01 2017/04/02 e così via, immettere adfblobconnector / / {year} / {month} / {day} per file o cartella.</span><span class="sxs-lookup"><span data-stu-id="39ba8-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="39ba8-421">Quando si preme TAB dalla casella di testo hello, vengono visualizzati tre formati di tooselect elenchi a discesa per anno (aaaa), month (MM) e giorno (gg).</span><span class="sxs-lookup"><span data-stu-id="39ba8-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="39ba8-422">Non impostare **Copy file recursively** (Copia file in modo ricorsivo).</span><span class="sxs-lookup"><span data-stu-id="39ba8-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="39ba8-423">Selezionare questo incrociato toorecursively opzione all'interno delle cartelle per i file toobe toohello copiato di destinazione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="39ba8-424">Non hello **copia binaria** opzione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="39ba8-425">Selezionare questo tooperform opzione una copia binaria della destinazione toohello file di origine.</span><span class="sxs-lookup"><span data-stu-id="39ba8-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="39ba8-426">Non selezionare per questa procedura dettagliata in modo che è possibile visualizzare altre opzioni nelle pagine successive hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="39ba8-427">Verificare che hello **tipo di compressione** è troppo**Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="39ba8-428">Selezionare un valore per questa opzione se i file di origine vengono compressi in uno dei formati di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="39ba8-429">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-429">Click **Next**.</span></span>
    <span data-ttu-id="39ba8-430">![Strumento Copia - scegliere i file di input hello o cartella](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="39ba8-431">In hello **impostazioni del File di formato** visualizzata delimitatori hello e lo schema di hello che viene rilevata automaticamente dalla procedura guidata hello mediante l'analisi di file hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="39ba8-432">Confermare le opzioni seguenti hello: una.</span><span class="sxs-lookup"><span data-stu-id="39ba8-432">Confirm hello following options: a.</span></span> <span data-ttu-id="39ba8-433">Hello **formato** è troppo**formato testo**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="39ba8-434">È possibile visualizzare tutti i formati di hello è supportato nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="39ba8-435">Ad esempio: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="39ba8-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="39ba8-436">b.</span><span class="sxs-lookup"><span data-stu-id="39ba8-436">b.</span></span> <span data-ttu-id="39ba8-437">Hello **delimitatore di colonna** è troppo`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="39ba8-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="39ba8-438">È possibile visualizzare hello altri delimitatori di colonna nell'elenco a discesa hello è supportati da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="39ba8-439">È anche possibile specificare un delimitatore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="39ba8-440">c.</span><span class="sxs-lookup"><span data-stu-id="39ba8-440">c.</span></span> <span data-ttu-id="39ba8-441">Hello **delimitatore di riga** è troppo`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="39ba8-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="39ba8-442">È possibile visualizzare hello altri delimitatori di riga nell'elenco a discesa hello è supportati da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="39ba8-443">È anche possibile specificare un delimitatore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="39ba8-444">d.</span><span class="sxs-lookup"><span data-stu-id="39ba8-444">d.</span></span> <span data-ttu-id="39ba8-445">Hello **ignorare conteggio delle righe** è troppo**0**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="39ba8-446">Se si desidera qualche toobe righe ignorate all'inizio di hello del file hello, immettere il numero di hello qui.</span><span class="sxs-lookup"><span data-stu-id="39ba8-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="39ba8-447">e.</span><span class="sxs-lookup"><span data-stu-id="39ba8-447">e.</span></span>  <span data-ttu-id="39ba8-448">Hello **prima riga di dati contiene nomi di colonna** non è impostata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="39ba8-449">Se il file di origine hello contengono nomi di colonna nella prima riga hello, selezionare questa opzione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="39ba8-450">f.</span><span class="sxs-lookup"><span data-stu-id="39ba8-450">f.</span></span> <span data-ttu-id="39ba8-451">Hello **considerare il valore di colonna vuota come null** opzione è impostata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="39ba8-452">Espandere **impostazioni avanzate** toosee disponibili opzioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="39ba8-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="39ba8-453">Nella parte inferiore di hello della pagina hello, vedere hello **anteprima** di dati da file emp.txt hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="39ba8-454">Fare clic su **SCHEMA** scheda in schema di hello inferiore toosee hello tale procedura guidata copia hello dedotto osservando i dati di hello nel file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="39ba8-455">Fare clic su **Avanti** dopo aver esaminato i delimitatori di hello e anteprima dei dati.</span><span class="sxs-lookup"><span data-stu-id="39ba8-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="39ba8-456">![Strumento di copia - Impostazioni di formattazioni del file](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="39ba8-457">In hello **memorizzazione di dati di destinazione della pagina**selezionare **archiviazione Blob di Azure**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="39ba8-458">Si utilizza hello archiviazione Blob di Azure come entrambi hello origine e destinazione gli archivi dati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="39ba8-459">![Strumento di copia - Selezionare l'archivio dati di destinazione](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="39ba8-460">In **specificare account di archiviazione Blob di Azure hello** pagina:</span><span class="sxs-lookup"><span data-stu-id="39ba8-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="39ba8-461">Immettere **AzureStorageLinkedService** per hello **nome connessione** campo.</span><span class="sxs-lookup"><span data-stu-id="39ba8-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="39ba8-462">Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="39ba8-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="39ba8-463">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="39ba8-464">Selezionare l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="39ba8-465">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-465">Click **Next**.</span></span>     
10. <span data-ttu-id="39ba8-466">In hello **hello Scegli file o una cartella di output** pagina:</span><span class="sxs-lookup"><span data-stu-id="39ba8-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="39ba8-467">In **Percorso cartella** specificare **adfblobconnector/output/{year}/{month}/{day}** (adfblobconnector/output/{anno}/{mese}/{giorno}).</span><span class="sxs-lookup"><span data-stu-id="39ba8-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="39ba8-468">Premere **TAB**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="39ba8-469">Per hello **anno**selezionare **aaaa**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="39ba8-470">Per hello **mese**, verificare che sia impostato troppo**MM**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="39ba8-471">Per hello **giorno**, verificare che sia impostato troppo**gg**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="39ba8-472">Verificare che hello **tipo di compressione** è troppo**Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="39ba8-473">Verificare che hello **copiare comportamento** è troppo**unire file**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="39ba8-474">Se l'output di hello file con hello stesso nome esiste già, hello nuovo contenuto è toohello aggiunto lo stesso file alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="39ba8-475">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-475">Click **Next**.</span></span>
    <span data-ttu-id="39ba8-476">![Strumento di copia - Scegliere il file o la cartella di output](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="39ba8-477">In hello **impostazioni del File di formato** pagina, rivedere le impostazioni di hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="39ba8-478">Una delle opzioni aggiuntive di hello qui è un file di output intestazione toohello tooadd.</span><span class="sxs-lookup"><span data-stu-id="39ba8-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="39ba8-479">Se si seleziona questa opzione, viene aggiunta una riga di intestazione con nomi di colonne hello dallo schema hello dell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="39ba8-480">È possibile rinominare i nomi di colonna predefiniti hello durante la visualizzazione schema hello hello origine.</span><span class="sxs-lookup"><span data-stu-id="39ba8-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="39ba8-481">Ad esempio, è possibile modificare hello prima colonna tooFirst nome e secondo tooLast colonna nome.</span><span class="sxs-lookup"><span data-stu-id="39ba8-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="39ba8-482">Quindi, viene generato il file di output di hello con un'intestazione con questi nomi come nomi di colonna.</span><span class="sxs-lookup"><span data-stu-id="39ba8-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="39ba8-483">![Strumento di copia - Impostazioni di formatto file per la destinazione](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="39ba8-484">In hello **le impostazioni delle prestazioni** pagina, verificare che **cloud unità** e **parallela copie** sono troppo**automatica**, fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="39ba8-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="39ba8-485">Per informazioni dettagliate su queste impostazioni, vedere [Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="39ba8-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="39ba8-486">![Strumento di copia - Impostazioni relative alle prestazioni](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="39ba8-487">In hello **riepilogo** pagina, esaminare tutte le impostazioni di protezione (le proprietà dell'attività, le impostazioni per l'origine e di destinazione e le impostazioni di copia) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="39ba8-488">![Strumento di copia - Pagina Riepilogo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="39ba8-489">Esaminare le informazioni nella hello **riepilogo** pagina e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="39ba8-490">procedura guidata di Hello crea due servizi collegati, due set di dati (input e output) e una pipeline in data factory di hello (dalla quale è stata avviata la procedura guidata copia hello).</span><span class="sxs-lookup"><span data-stu-id="39ba8-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="39ba8-491">![Strumento di copia - Pagina di distribuzione](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="39ba8-492">Pipeline di hello monitoraggio (attività di copia)</span><span class="sxs-lookup"><span data-stu-id="39ba8-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="39ba8-493">Fare clic sul collegamento hello `Click here toomonitor copy pipeline` su hello **distribuzione** pagina.</span><span class="sxs-lookup"><span data-stu-id="39ba8-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="39ba8-494">Dovrebbe essere hello **monitorare e gestire applicazioni** in una scheda separata.  ![App Monitoraggio e gestione](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="39ba8-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="39ba8-495">Hello modifica **avviare** tempo nella parte superiore di hello troppo`04/19/2017` e **fine** troppo tempo`04/27/2017`, quindi fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="39ba8-496">Dovrebbe essere cinque le finestre attività in hello **attività WINDOWS** elenco.</span><span class="sxs-lookup"><span data-stu-id="39ba8-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="39ba8-497">Hello **WindowStart** volte dovrebbero coprire tutti i giorni dall'ora di fine toopipeline di inizio della pipeline.</span><span class="sxs-lookup"><span data-stu-id="39ba8-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="39ba8-498">Fare clic su **aggiornamento** pulsante per hello **attività WINDOWS** elenco più volte fino a visualizzare lo stato di hello di tutte le finestre attività hello è tooReady.</span><span class="sxs-lookup"><span data-stu-id="39ba8-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="39ba8-499">A questo punto, verificare che nella cartella di output di hello del contenitore adfblobconnector vengono generati file di output di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="39ba8-500">È necessario visualizzare hello seguente struttura di cartelle nella cartella di output di hello:</span><span class="sxs-lookup"><span data-stu-id="39ba8-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="39ba8-501">Per informazioni dettagliate sul monitoraggio e la gestione delle data factory, vedere l'articolo [Monitorare e gestire le pipeline di Data Factory](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="39ba8-502">Entità di Data factory</span><span class="sxs-lookup"><span data-stu-id="39ba8-502">Data Factory entities</span></span>
<span data-ttu-id="39ba8-503">A questo punto, passare toohello back-scheda home page di hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="39ba8-504">Si noti che ora nella data factory sono presenti due servizi collegati, due set di dati e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="39ba8-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Home page di Data Factory con entità](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="39ba8-506">Fare clic su **autore e distribuire** toolaunch Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Editor di Data factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="39ba8-508">È necessario visualizzare hello dopo la data factory di entità Data Factory:</span><span class="sxs-lookup"><span data-stu-id="39ba8-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="39ba8-509">Due servizi collegati,</span><span class="sxs-lookup"><span data-stu-id="39ba8-509">Two linked services.</span></span> <span data-ttu-id="39ba8-510">Uno per l'origine di hello e hello un'altra destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="39ba8-511">Entrambi i servizi collegato hello vedere toohello stesso account di archiviazione di Azure in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="39ba8-512">Due set di dati,</span><span class="sxs-lookup"><span data-stu-id="39ba8-512">Two datasets.</span></span> <span data-ttu-id="39ba8-513">uno di input e uno di output.</span><span class="sxs-lookup"><span data-stu-id="39ba8-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="39ba8-514">In questa procedura dettagliata, entrambi utilizzano hello stesso contenitore di blob, ma fare riferimento a cartelle toodifferent (input e output).</span><span class="sxs-lookup"><span data-stu-id="39ba8-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="39ba8-515">Una pipeline.</span><span class="sxs-lookup"><span data-stu-id="39ba8-515">A pipeline.</span></span> <span data-ttu-id="39ba8-516">pipeline Hello contiene un'attività di copia che utilizza un'origine blob e un blob sink toocopy di dati da un tooanother percorso blob di Azure percorso blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="39ba8-517">Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su queste entità.</span><span class="sxs-lookup"><span data-stu-id="39ba8-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="39ba8-518">Servizi collegati</span><span class="sxs-lookup"><span data-stu-id="39ba8-518">Linked services</span></span>
<span data-ttu-id="39ba8-519">Verranno visualizzati due servizi collegati,</span><span class="sxs-lookup"><span data-stu-id="39ba8-519">You should see two linked services.</span></span> <span data-ttu-id="39ba8-520">Uno per l'origine di hello e hello un'altra destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="39ba8-521">In questa procedura dettagliata, entrambe le definizioni di aspetto hello stessa ad eccezione dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="39ba8-522">Hello **tipo** di hello servizio collegato è troppo**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="39ba8-523">Proprietà più importante della definizione di servizio collegato hello è hello **connectionString**, che viene utilizzato da Data Factory tooconnect tooyour account di archiviazione di Azure in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="39ba8-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="39ba8-524">Proprietà hubName hello nella definizione di hello ignorata.</span><span class="sxs-lookup"><span data-stu-id="39ba8-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="39ba8-525">Servizio collegato di archiviazione BLOB di origine</span><span class="sxs-lookup"><span data-stu-id="39ba8-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="39ba8-526">Servizio collegato di archiviazione BLOB di destinazione</span><span class="sxs-lookup"><span data-stu-id="39ba8-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="39ba8-527">Per altre informazioni sui servizi collegati di archiviazione di Azure, vedere la sezione [Proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="39ba8-528">Set di dati</span><span class="sxs-lookup"><span data-stu-id="39ba8-528">Datasets</span></span>
<span data-ttu-id="39ba8-529">Sono presenti due set di dati, uno di input e uno di output.</span><span class="sxs-lookup"><span data-stu-id="39ba8-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="39ba8-530">tipo di Hello del set di dati hello è impostato troppo**AzureBlob** per entrambi.</span><span class="sxs-lookup"><span data-stu-id="39ba8-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="39ba8-531">set di dati input Hello punta toohello **input** cartella di hello **adfblobconnector** contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="39ba8-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="39ba8-532">Hello **esterno** impostata troppo**true** per questo set di dati come hello dati non viene generati dalla pipeline hello con attività di copia hello che accetta questo set di dati come input.</span><span class="sxs-lookup"><span data-stu-id="39ba8-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="39ba8-533">toohello punti set di dati di output di Hello **output** cartella di hello stesso contenitore di blob.</span><span class="sxs-lookup"><span data-stu-id="39ba8-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="39ba8-534">Hello set di dati di output utilizza inoltre hello anno, mese e giorno di hello **SliceStart** toodynamically variabile di sistema valutare hello percorso hello file di output.</span><span class="sxs-lookup"><span data-stu-id="39ba8-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="39ba8-535">Per un elenco di funzioni e variabili di sistema supportate da Data Factory, vedere l'articolo [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="39ba8-536">Hello **esterno** impostata troppo**false** (valore predefinito) perché questo set di dati viene generato dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="39ba8-537">Per altre informazioni sulle proprietà supportate dal set di dati del BLOB di Azure, vedere la sezione [Proprietà dei set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="39ba8-538">Set di dati di input</span><span class="sxs-lookup"><span data-stu-id="39ba8-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="39ba8-539">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="39ba8-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="39ba8-540">Pipeline</span><span class="sxs-lookup"><span data-stu-id="39ba8-540">Pipeline</span></span>
<span data-ttu-id="39ba8-541">pipeline Hello è semplicemente un'attività.</span><span class="sxs-lookup"><span data-stu-id="39ba8-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="39ba8-542">Hello **tipo** di hello attività è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="39ba8-543">In proprietà del tipo hello per attività hello, sono presenti due sezioni, una per l'origine e di hello un'altra per il sink.</span><span class="sxs-lookup"><span data-stu-id="39ba8-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="39ba8-544">tipo di origine Hello è troppo**BlobSource** come attività hello sta copiando i dati da un'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="39ba8-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="39ba8-545">Hello il tipo di sink è impostato troppo**BlobSink** come attività hello la copia di archiviazione blob di dati tooa.</span><span class="sxs-lookup"><span data-stu-id="39ba8-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="39ba8-546">attività di copia Hello accetta InputDataset z4y come input hello e OutputDataset-z4y come output di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="39ba8-547">Per altre informazioni sulle proprietà supportate da BlobSource e BlobSink, vedere la sezione [Proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="39ba8-548">Esempi JSON per la copia dei dati tooand dall'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="39ba8-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="39ba8-549">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="39ba8-550">Vengono visualizzate come toocopy tooand di dati dall'archiviazione Blob di Azure e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="39ba8-551">Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39ba8-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="39ba8-552">Esempio JSON: Copiare i dati da archiviazione Blob tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="39ba8-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="39ba8-553">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="39ba8-553">hello following sample shows:</span></span>

1. <span data-ttu-id="39ba8-554">Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="39ba8-555">Un servizio collegato di tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="39ba8-556">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="39ba8-557">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="39ba8-558">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="39ba8-559">esempio Hello copia i dati delle serie temporali da una tabella di SQL Azure tooan blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="39ba8-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="39ba8-560">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="39ba8-561">**Servizio collegato SQL di Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="39ba8-562">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="39ba8-563">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="39ba8-564">Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="39ba8-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="39ba8-565">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="39ba8-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="39ba8-566">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="39ba8-567">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="39ba8-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="39ba8-568">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="39ba8-569">percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="39ba8-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="39ba8-570">"external": "true" impostazione informa Data Factory di tale tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="39ba8-571">**Set di dati di output SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="39ba8-572">esempio Hello copia tabella tooa dati denominata "MyTable" in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba8-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="39ba8-573">Crea tabella hello nel database SQL di Azure con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="39ba8-574">Aggiunta di nuove righe nella tabella toohello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="39ba8-574">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="39ba8-575">**Un'attività di copia in una pipeline con un'origine BLOB e un sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="39ba8-576">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="39ba8-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="39ba8-577">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="39ba8-578">Esempio JSON: Copiare i dati da SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="39ba8-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="39ba8-579">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="39ba8-579">hello following sample shows:</span></span>

1. <span data-ttu-id="39ba8-580">Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="39ba8-581">Un servizio collegato di tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="39ba8-582">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="39ba8-583">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="39ba8-584">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39ba8-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="39ba8-585">esempio Hello copia i dati delle serie temporali da un tooan tabella SQL di Azure blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="39ba8-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="39ba8-586">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="39ba8-587">**Servizio collegato SQL di Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="39ba8-588">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="39ba8-589">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="39ba8-590">Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="39ba8-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="39ba8-591">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="39ba8-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="39ba8-592">**Set di dati di input SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="39ba8-593">esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Azure e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="39ba8-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="39ba8-594">L'impostazione "external": "true" informa il servizio Data Factory tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="39ba8-595">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="39ba8-596">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="39ba8-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="39ba8-597">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="39ba8-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="39ba8-598">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="39ba8-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="39ba8-599">**Un'attività di copia in una pipeline con un'origine SQL e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="39ba8-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="39ba8-600">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="39ba8-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="39ba8-601">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="39ba8-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="39ba8-602">query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="39ba8-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="39ba8-603">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="39ba8-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="39ba8-604">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="39ba8-604">Performance and Tuning</span></span>
<span data-ttu-id="39ba8-605">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="39ba8-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
