---
title: aaaMove dati da e verso tabelle di Azure | Documenti Microsoft
description: Informazioni su come toomove dati in o dall'archiviazione tabelle di Azure usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="64f72-103">Spostare dati tooand dalla tabella di Azure usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="64f72-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="64f72-104">Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove a/da Archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="64f72-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="64f72-106">È possibile copiare dati da qualsiasi origine supportati dati archiviano tooAzure archiviazione tabelle o da dati di archiviazione tabelle di Azure supportata tooany sink archivio.</span><span class="sxs-lookup"><span data-stu-id="64f72-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="64f72-107">Per un elenco di archivi dati come origini o sink è supportato dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="64f72-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="64f72-108">introduttiva</span><span class="sxs-lookup"><span data-stu-id="64f72-108">Getting started</span></span>
<span data-ttu-id="64f72-109">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un'archiviazione tabelle di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="64f72-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="64f72-110">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="64f72-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="64f72-111">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="64f72-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="64f72-112">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="64f72-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="64f72-113">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="64f72-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="64f72-114">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="64f72-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="64f72-115">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="64f72-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="64f72-116">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="64f72-117">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="64f72-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="64f72-118">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="64f72-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="64f72-119">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="64f72-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="64f72-120">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati dati da e verso un archivio tabelle di Azure, vedere [esempi JSON](#json-examples) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="64f72-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="64f72-121">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure archiviazione tabelle:</span><span class="sxs-lookup"><span data-stu-id="64f72-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="64f72-122">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="64f72-122">Linked service properties</span></span>
<span data-ttu-id="64f72-123">Esistono due tipi di servizi collegati è possibile utilizzare toolink un blob di Azure storage tooan data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="64f72-124">I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="64f72-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="64f72-125">Hello servizio collegato di archiviazione di Azure fornisce data factory di hello con accesso globale toohello di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="64f72-126">Mentre, hello Azure archiviazione SAS (firma di accesso condiviso) collegati servizio fornisce data factory di hello con accesso limitato/scadenza toohello di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="64f72-127">Non esistono altre differenze tra questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="64f72-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="64f72-128">Scegliere servizio hello collegato alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="64f72-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="64f72-129">Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="64f72-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="64f72-130">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="64f72-130">Dataset properties</span></span>
<span data-ttu-id="64f72-131">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="64f72-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="64f72-132">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="64f72-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="64f72-133">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="64f72-134">Hello **typeProperties** sezione per hello set di dati di tipo **AzureTable** è hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="64f72-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="64f72-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="64f72-135">Property</span></span> | <span data-ttu-id="64f72-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="64f72-136">Description</span></span> | <span data-ttu-id="64f72-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="64f72-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64f72-138">tableName</span><span class="sxs-lookup"><span data-stu-id="64f72-138">tableName</span></span> |<span data-ttu-id="64f72-139">Nome della tabella hello nell'istanza di Database della tabella di Azure hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="64f72-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="64f72-140">Sì.</span><span class="sxs-lookup"><span data-stu-id="64f72-140">Yes.</span></span> <span data-ttu-id="64f72-141">Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="64f72-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="64f72-142">Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="64f72-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="64f72-143">Schema da Data Factory</span><span class="sxs-lookup"><span data-stu-id="64f72-143">Schema by Data Factory</span></span>
<span data-ttu-id="64f72-144">Per gli archivi dati privi di schema, ad esempio tabelle di Azure, servizio Data Factory hello viene dedotto schema hello in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="64f72-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="64f72-145">Se si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, hello servizio Data Factory rispetta questa struttura come schema hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="64f72-146">In questo caso, se una riga non contiene un valore per una colonna, viene inserito un valore null.</span><span class="sxs-lookup"><span data-stu-id="64f72-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="64f72-147">Se non si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, Data Factory di inferenza dello schema di hello utilizzando prima riga hello nei dati hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="64f72-148">In questo caso, se hello prima riga contiene schema completo hello, alcune colonne vengono persi nel risultato hello dell'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="64f72-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="64f72-149">Pertanto, per le origini dati privi di schema consigliata hello è struttura hello toospecify dei dati tramite hello **struttura** proprietà.</span><span class="sxs-lookup"><span data-stu-id="64f72-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="64f72-150">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="64f72-150">Copy activity properties</span></span>
<span data-ttu-id="64f72-151">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="64f72-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="64f72-152">Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="64f72-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="64f72-153">Le proprietà disponibili nella sezione typeProperties hello di attività hello hello invece variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="64f72-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="64f72-154">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="64f72-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="64f72-155">**AzureTableSource** supporta hello le proprietà nella sezione typeProperties seguenti:</span><span class="sxs-lookup"><span data-stu-id="64f72-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="64f72-156">Proprietà</span><span class="sxs-lookup"><span data-stu-id="64f72-156">Property</span></span> | <span data-ttu-id="64f72-157">Descrizione</span><span class="sxs-lookup"><span data-stu-id="64f72-157">Description</span></span> | <span data-ttu-id="64f72-158">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="64f72-158">Allowed values</span></span> | <span data-ttu-id="64f72-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="64f72-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64f72-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="64f72-160">azureTableSourceQuery</span></span> |<span data-ttu-id="64f72-161">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="64f72-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="64f72-162">Stringa di query della tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-162">Azure table query string.</span></span> <span data-ttu-id="64f72-163">Vedere gli esempi nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-163">See examples in hello next section.</span></span> |<span data-ttu-id="64f72-164">No.</span><span class="sxs-lookup"><span data-stu-id="64f72-164">No.</span></span> <span data-ttu-id="64f72-165">Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="64f72-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="64f72-166">Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="64f72-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="64f72-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="64f72-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="64f72-168">Indica se ignorare hello eccezione della tabella non esiste.</span><span class="sxs-lookup"><span data-stu-id="64f72-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="64f72-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="64f72-169">TRUE</span></span><br/><span data-ttu-id="64f72-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="64f72-170">FALSE</span></span> |<span data-ttu-id="64f72-171">No</span><span class="sxs-lookup"><span data-stu-id="64f72-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="64f72-172">esempi di azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="64f72-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="64f72-173">Se la colonna della tabella di Azure è di tipo stringa:</span><span class="sxs-lookup"><span data-stu-id="64f72-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="64f72-174">Se la colonna della tabella di Azure è di tipo datetime:</span><span class="sxs-lookup"><span data-stu-id="64f72-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="64f72-175">**AzureTableSink** supporta hello le proprietà nella sezione typeProperties seguenti:</span><span class="sxs-lookup"><span data-stu-id="64f72-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="64f72-176">Proprietà</span><span class="sxs-lookup"><span data-stu-id="64f72-176">Property</span></span> | <span data-ttu-id="64f72-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="64f72-177">Description</span></span> | <span data-ttu-id="64f72-178">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="64f72-178">Allowed values</span></span> | <span data-ttu-id="64f72-179">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="64f72-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64f72-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="64f72-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="64f72-181">Partizione chiave valore predefinito che può essere usato dal sink hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="64f72-182">Valore stringa.</span><span class="sxs-lookup"><span data-stu-id="64f72-182">A string value.</span></span> |<span data-ttu-id="64f72-183">No</span><span class="sxs-lookup"><span data-stu-id="64f72-183">No</span></span> |
| <span data-ttu-id="64f72-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="64f72-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="64f72-185">Nome della colonna hello i cui valori vengono utilizzati come chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="64f72-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="64f72-186">Se non specificato, AzureTableDefaultPartitionKeyValue viene utilizzato come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="64f72-187">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="64f72-187">A column name.</span></span> |<span data-ttu-id="64f72-188">No</span><span class="sxs-lookup"><span data-stu-id="64f72-188">No</span></span> |
| <span data-ttu-id="64f72-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="64f72-189">azureTableRowKeyName</span></span> |<span data-ttu-id="64f72-190">Nome della colonna hello i cui valori di colonna vengono utilizzati come chiave di riga.</span><span class="sxs-lookup"><span data-stu-id="64f72-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="64f72-191">Se non specificato, usare un GUID per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="64f72-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="64f72-192">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="64f72-192">A column name.</span></span> |<span data-ttu-id="64f72-193">No</span><span class="sxs-lookup"><span data-stu-id="64f72-193">No</span></span> |
| <span data-ttu-id="64f72-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="64f72-194">azureTableInsertType</span></span> |<span data-ttu-id="64f72-195">Hello modalità tooinsert i dati in tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="64f72-196">Questa proprietà controlla se le righe esistenti nella tabella di output di hello con le chiavi di riga e di partizione corrispondenti hanno valori di sostituzione o unione.</span><span class="sxs-lookup"><span data-stu-id="64f72-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="64f72-197">toolearn sul funzionano di queste impostazioni (merge e la sostituzione), vedere [Insert o l'entità di tipo Merge](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [Insert o sostituire entità](https://msdn.microsoft.com/library/azure/hh452242.aspx) argomenti.</span><span class="sxs-lookup"><span data-stu-id="64f72-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="64f72-198">Questa impostazione si applica a livello di riga hello, non a livello tabella hello, e nessuna delle due opzioni consente di eliminare le righe nella tabella di output di hello che non esistono nell'input hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="64f72-199">merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="64f72-199">merge (default)</span></span><br/><span data-ttu-id="64f72-200">replace</span><span class="sxs-lookup"><span data-stu-id="64f72-200">replace</span></span> |<span data-ttu-id="64f72-201">No</span><span class="sxs-lookup"><span data-stu-id="64f72-201">No</span></span> |
| <span data-ttu-id="64f72-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="64f72-202">writeBatchSize</span></span> |<span data-ttu-id="64f72-203">Inserisce dati nella tabella di Azure hello quando hello di viene raggiunto writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="64f72-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="64f72-204">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="64f72-204">Integer (number of rows)</span></span> |<span data-ttu-id="64f72-205">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="64f72-205">No (default: 10000)</span></span> |
| <span data-ttu-id="64f72-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="64f72-206">writeBatchTimeout</span></span> |<span data-ttu-id="64f72-207">Inserisce i dati in tabelle di Azure hello quando viene raggiunto writeBatchSize hello o writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="64f72-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="64f72-208">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="64f72-208">timespan</span></span><br/><br/><span data-ttu-id="64f72-209">Ad esempio: "00:20:00" (20 minuti)</span><span class="sxs-lookup"><span data-stu-id="64f72-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="64f72-210">No (valore di timeout predefinito del client predefinito toostorage 90 secondi)</span><span class="sxs-lookup"><span data-stu-id="64f72-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="64f72-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="64f72-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="64f72-212">Eseguire il mapping di una colonna di destinazione tooa colonna di origine utilizzando proprietà JSON traduttore hello prima di poter utilizzare le colonne di destinazione hello come hello azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="64f72-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="64f72-213">Nell'esempio seguente di hello, la colonna di origine DivisionID è la colonna di destinazione mappata toohello: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="64f72-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="64f72-214">Hello DivisionID viene specificato come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="64f72-215">Esempi JSON</span><span class="sxs-lookup"><span data-stu-id="64f72-215">JSON examples</span></span>
<span data-ttu-id="64f72-216">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="64f72-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="64f72-217">Vengono visualizzate come toocopy tooand di dati da Archiviazione tabelle di Azure e Database di Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="64f72-218">Tuttavia, i dati possono essere copiati **direttamente** da qualsiasi hello origini tooany di sink hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="64f72-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="64f72-219">Per ulteriori informazioni, vedere sezione hello "archivi di dati supportati e formati" in [spostare i dati utilizzando l'attività di copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="64f72-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="64f72-220">Esempio: Copiare i dati da tabelle di Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="64f72-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="64f72-221">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="64f72-221">hello following sample shows:</span></span>

1. <span data-ttu-id="64f72-222">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).</span><span class="sxs-lookup"><span data-stu-id="64f72-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="64f72-223">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64f72-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="64f72-224">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64f72-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="64f72-225">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="64f72-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="64f72-226">esempio Hello copia i dati appartenenti a partizione predefinita toohello in un blob tooa tabelle di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="64f72-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="64f72-227">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="64f72-228">**Servizio collegato di archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="64f72-228">**Azure storage linked service:**</span></span>

```JSON
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
<span data-ttu-id="64f72-229">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="64f72-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="64f72-230">Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="64f72-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="64f72-231">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="64f72-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="64f72-232">**Set di dati di input di tabelle di Azure**</span><span class="sxs-lookup"><span data-stu-id="64f72-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="64f72-233">esempio Hello presuppone di che aver creato una tabella "MyTable" nella tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="64f72-234">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="64f72-235">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="64f72-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="64f72-236">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="64f72-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="64f72-237">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="64f72-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="64f72-238">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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

<span data-ttu-id="64f72-239">**Attività di copia in una pipeline con AzureTableSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="64f72-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="64f72-240">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="64f72-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="64f72-241">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**AzureTableSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="64f72-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="64f72-242">query SQL Hello specificata con **AzureTableSourceQuery** proprietà consente di selezionare dati hello dalla partizione predefinita hello toocopy ogni ora.</span><span class="sxs-lookup"><span data-stu-id="64f72-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="64f72-243">Esempio: Copiare i dati da Blob di Azure tooAzure tabella</span><span class="sxs-lookup"><span data-stu-id="64f72-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="64f72-244">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="64f72-244">hello following sample shows:</span></span>

1. <span data-ttu-id="64f72-245">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).</span><span class="sxs-lookup"><span data-stu-id="64f72-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="64f72-246">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64f72-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="64f72-247">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64f72-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="64f72-248">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="64f72-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="64f72-249">esempio Hello copia i dati delle serie temporali da una tabella di Azure di tooan blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="64f72-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="64f72-250">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="64f72-251">**Servizio collegato di Archiviazione di Azure (per tabelle di Azure e BLOB):**</span><span class="sxs-lookup"><span data-stu-id="64f72-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

```JSON
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

<span data-ttu-id="64f72-252">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="64f72-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="64f72-253">Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="64f72-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="64f72-254">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="64f72-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="64f72-255">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="64f72-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="64f72-256">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="64f72-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="64f72-257">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="64f72-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="64f72-258">percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="64f72-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="64f72-259">"external": "true" impostazione informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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

<span data-ttu-id="64f72-260">**Set di dati di output di tabelle di Azure**</span><span class="sxs-lookup"><span data-stu-id="64f72-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="64f72-261">esempio Hello copia tabella tooa dati denominata "MyTable" nella tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="64f72-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="64f72-262">Creare una tabella di Azure con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="64f72-263">Aggiunta di nuove righe nella tabella toohello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="64f72-263">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="64f72-264">**Copiare attività in una pipeline con BlobSource e AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="64f72-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="64f72-265">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="64f72-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="64f72-266">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="64f72-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="64f72-267">Mapping dei tipi per tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="64f72-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="64f72-268">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="64f72-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="64f72-269">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="64f72-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="64f72-270">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="64f72-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="64f72-271">Quando si spostano dati troppo & dalla tabella di Azure, hello seguente [mapping definiti dal servizio tabelle di Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) vengono utilizzati dal tipo di too.NET tipi OData di tabella di Azure e viceversa.</span><span class="sxs-lookup"><span data-stu-id="64f72-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="64f72-272">Tipo di dati OData</span><span class="sxs-lookup"><span data-stu-id="64f72-272">OData Data Type</span></span> | <span data-ttu-id="64f72-273">Tipo di .NET</span><span class="sxs-lookup"><span data-stu-id="64f72-273">.NET Type</span></span> | <span data-ttu-id="64f72-274">Dettagli</span><span class="sxs-lookup"><span data-stu-id="64f72-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64f72-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="64f72-275">Edm.Binary</span></span> |<span data-ttu-id="64f72-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="64f72-276">byte[]</span></span> |<span data-ttu-id="64f72-277">Matrice di byte too64 KB.</span><span class="sxs-lookup"><span data-stu-id="64f72-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="64f72-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="64f72-278">Edm.Boolean</span></span> |<span data-ttu-id="64f72-279">bool</span><span class="sxs-lookup"><span data-stu-id="64f72-279">bool</span></span> |<span data-ttu-id="64f72-280">Valore booleano.</span><span class="sxs-lookup"><span data-stu-id="64f72-280">A Boolean value.</span></span> |
| <span data-ttu-id="64f72-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="64f72-281">Edm.DateTime</span></span> |<span data-ttu-id="64f72-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="64f72-282">DateTime</span></span> |<span data-ttu-id="64f72-283">Un valore a 64 bit espresso come Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="64f72-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="64f72-284">Hello supportato DateTime intervallo inizia a mezzanotte, 1 gennaio 1601 D.C.</span><span class="sxs-lookup"><span data-stu-id="64f72-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="64f72-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="64f72-285">(C.E.), UTC.</span></span> <span data-ttu-id="64f72-286">Hello intervallo termina il 31 dicembre 9999.</span><span class="sxs-lookup"><span data-stu-id="64f72-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="64f72-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="64f72-287">Edm.Double</span></span> |<span data-ttu-id="64f72-288">double</span><span class="sxs-lookup"><span data-stu-id="64f72-288">double</span></span> |<span data-ttu-id="64f72-289">Un valore a virgola mobile a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="64f72-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="64f72-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="64f72-290">Edm.Guid</span></span> |<span data-ttu-id="64f72-291">Guid</span><span class="sxs-lookup"><span data-stu-id="64f72-291">Guid</span></span> |<span data-ttu-id="64f72-292">Un identificatore univoco globale a 128 bit.</span><span class="sxs-lookup"><span data-stu-id="64f72-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="64f72-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="64f72-293">Edm.Int32</span></span> |<span data-ttu-id="64f72-294">Int32</span><span class="sxs-lookup"><span data-stu-id="64f72-294">Int32</span></span> |<span data-ttu-id="64f72-295">Un valore integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="64f72-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="64f72-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="64f72-296">Edm.Int64</span></span> |<span data-ttu-id="64f72-297">Int64</span><span class="sxs-lookup"><span data-stu-id="64f72-297">Int64</span></span> |<span data-ttu-id="64f72-298">Un valore integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="64f72-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="64f72-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="64f72-299">Edm.String</span></span> |<span data-ttu-id="64f72-300">String</span><span class="sxs-lookup"><span data-stu-id="64f72-300">String</span></span> |<span data-ttu-id="64f72-301">Un valore con codifica UTF-16.</span><span class="sxs-lookup"><span data-stu-id="64f72-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="64f72-302">I valori stringa possono essere too64 KB.</span><span class="sxs-lookup"><span data-stu-id="64f72-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="64f72-303">Esempio di conversione di tipo</span><span class="sxs-lookup"><span data-stu-id="64f72-303">Type Conversion Sample</span></span>
<span data-ttu-id="64f72-304">Dopo l'esempio Hello è per la copia di dati da una tabella di tooAzure Blob di Azure con conversioni del tipo.</span><span class="sxs-lookup"><span data-stu-id="64f72-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="64f72-305">Si supponga di set di dati Blob hello è in formato CSV e contiene tre colonne.</span><span class="sxs-lookup"><span data-stu-id="64f72-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="64f72-306">Uno di essi è una colonna datetime con un formato di data e ora personalizzate utilizzando nomi francesi abbreviati per giorno della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="64f72-307">Definire il set di dati di hello origine Blob come indicato di seguito, insieme a definizioni di tipo per le colonne di hello.</span><span class="sxs-lookup"><span data-stu-id="64f72-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="64f72-308">Dato il mapping dei tipi hello dal tipo di too.NET tipo OData di tabella di Azure, si definirebbe tabella hello in tabelle di Azure con hello seguente schema.</span><span class="sxs-lookup"><span data-stu-id="64f72-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="64f72-309">**Schema di tabelle di Azure:**</span><span class="sxs-lookup"><span data-stu-id="64f72-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="64f72-310">Nome colonna</span><span class="sxs-lookup"><span data-stu-id="64f72-310">Column name</span></span> | <span data-ttu-id="64f72-311">Tipo</span><span class="sxs-lookup"><span data-stu-id="64f72-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="64f72-312">userid</span><span class="sxs-lookup"><span data-stu-id="64f72-312">userid</span></span> |<span data-ttu-id="64f72-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="64f72-313">Edm.Int64</span></span> |
| <span data-ttu-id="64f72-314">name</span><span class="sxs-lookup"><span data-stu-id="64f72-314">name</span></span> |<span data-ttu-id="64f72-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="64f72-315">Edm.String</span></span> |
| <span data-ttu-id="64f72-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="64f72-316">lastlogindate</span></span> |<span data-ttu-id="64f72-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="64f72-317">Edm.DateTime</span></span> |

<span data-ttu-id="64f72-318">Successivamente, definire set di dati di hello tabelle di Azure come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="64f72-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="64f72-319">Sezione "struttura" toospecify con informazioni sul tipo hello non è necessario perché le informazioni sul tipo hello è già specificati in hello archivio dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="64f72-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="64f72-320">In questo caso, Data Factory automaticamente conversioni di tipi tra i campi Datetime hello con il formato di data e ora personalizzate hello utilizzando le impostazioni cultura "fr-fr" hello, quando si spostano dati da Blob tooAzure tabella.</span><span class="sxs-lookup"><span data-stu-id="64f72-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="64f72-321">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="64f72-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="64f72-322">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="64f72-322">Performance and Tuning</span></span>
<span data-ttu-id="64f72-323">toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize, vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="64f72-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
