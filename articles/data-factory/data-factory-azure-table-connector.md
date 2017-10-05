---
title: Spostare dati da e verso le tabelle di Azure | Documentazione Microsoft
description: Informazioni su come spostare i dati da e verso l'archiviazione tabelle di Azure mediante Data factory di Azure.
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
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="ec77b-103">Spostare dati da e verso le tabelle di Azure mediante Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="ec77b-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="ec77b-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso un'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="ec77b-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ec77b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="ec77b-106">È possibile copiare i dati da qualsiasi archivio dati di origine supportato a un'archiviazione tabelle di Azure o da un'archiviazione tabelle di Azure a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="ec77b-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="ec77b-107">Per un elenco degli archivi dati supportati come origini o sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ec77b-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="ec77b-108">Introduzione</span><span class="sxs-lookup"><span data-stu-id="ec77b-108">Getting started</span></span>
<span data-ttu-id="ec77b-109">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un'archiviazione tabelle di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="ec77b-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="ec77b-110">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ec77b-111">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="ec77b-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="ec77b-112">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ec77b-113">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ec77b-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ec77b-114">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="ec77b-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="ec77b-115">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="ec77b-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="ec77b-116">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="ec77b-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="ec77b-117">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="ec77b-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ec77b-118">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ec77b-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ec77b-119">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="ec77b-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ec77b-120">Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso un'archiviazione tabelle di Azure, vedere la sezione degli [esempi JSON](#json-examples) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ec77b-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="ec77b-121">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un'archiviazione tabelle di Azure:</span><span class="sxs-lookup"><span data-stu-id="ec77b-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ec77b-122">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="ec77b-122">Linked service properties</span></span>
<span data-ttu-id="ec77b-123">Esistono due tipi di servizi collegati, che consentono di collegare un archivio BLOB di Azure a una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="ec77b-124">I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="ec77b-125">Il servizio collegato Archiviazione di Azure garantisce alla data factory l'accesso globale ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="ec77b-126">Invece il servizio collegato Firma di accesso condiviso di Archiviazione di Azure garantisce alla data factory l'accesso limitato o a scadenza ad Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="ec77b-127">Non esistono altre differenze tra questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="ec77b-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="ec77b-128">Scegliere il servizio collegato più adatto alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="ec77b-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="ec77b-129">Le sezioni seguenti forniscono altri dettagli su questi due servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="ec77b-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="ec77b-130">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="ec77b-130">Dataset properties</span></span>
<span data-ttu-id="ec77b-131">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="ec77b-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ec77b-132">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="ec77b-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ec77b-133">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="ec77b-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ec77b-134">La sezione **typeProperties** per il set di dati di tipo **AzureTable** presenta le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="ec77b-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="ec77b-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ec77b-135">Property</span></span> | <span data-ttu-id="ec77b-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ec77b-136">Description</span></span> | <span data-ttu-id="ec77b-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ec77b-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec77b-138">tableName</span><span class="sxs-lookup"><span data-stu-id="ec77b-138">tableName</span></span> |<span data-ttu-id="ec77b-139">Nome della tabella nell'istanza del database di tabelle di Azure a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="ec77b-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="ec77b-140">Sì.</span><span class="sxs-lookup"><span data-stu-id="ec77b-140">Yes.</span></span> <span data-ttu-id="ec77b-141">Quando si specifica tableName senza azureTableSourceQuery, tutti i record della tabella vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="ec77b-142">Se si specifica anche azureTableSourceQuery, i record della tabella che soddisfa la query vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="ec77b-143">Schema da Data Factory</span><span class="sxs-lookup"><span data-stu-id="ec77b-143">Schema by Data Factory</span></span>
<span data-ttu-id="ec77b-144">Per gli archivi di dati privi di schema, ad esempio Tabella di Azure, il servizio Data Factory deduce lo schema in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ec77b-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="ec77b-145">Se si specifica la struttura dei dati usando la proprietà **structure** nella definizione del set di dati, il servizio Data Factory considera la struttura come schema.</span><span class="sxs-lookup"><span data-stu-id="ec77b-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="ec77b-146">In questo caso, se una riga non contiene un valore per una colonna, viene inserito un valore null.</span><span class="sxs-lookup"><span data-stu-id="ec77b-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="ec77b-147">Se non si specifica la struttura dei dati usando la proprietà **structure** nella definizione del set di dati, Data Factory deduce lo schema usando la prima riga di dati.</span><span class="sxs-lookup"><span data-stu-id="ec77b-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="ec77b-148">In questo caso, se la prima riga non contiene lo schema completo, alcune colonne non sono presenti nel risultato dell'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="ec77b-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="ec77b-149">Di conseguenza, per le origini dati prive di schema, la procedura consigliata consiste nello specificare la struttura dei dati usando la proprietà **structure** .</span><span class="sxs-lookup"><span data-stu-id="ec77b-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="ec77b-150">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="ec77b-150">Copy activity properties</span></span>
<span data-ttu-id="ec77b-151">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ec77b-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ec77b-152">Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="ec77b-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="ec77b-153">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="ec77b-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="ec77b-154">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="ec77b-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="ec77b-155">**AzureTableSource** supporta le seguenti proprietà della sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="ec77b-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="ec77b-156">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ec77b-156">Property</span></span> | <span data-ttu-id="ec77b-157">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ec77b-157">Description</span></span> | <span data-ttu-id="ec77b-158">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="ec77b-158">Allowed values</span></span> | <span data-ttu-id="ec77b-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ec77b-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec77b-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="ec77b-160">azureTableSourceQuery</span></span> |<span data-ttu-id="ec77b-161">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="ec77b-161">Use the custom query to read data.</span></span> |<span data-ttu-id="ec77b-162">Stringa di query della tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-162">Azure table query string.</span></span> <span data-ttu-id="ec77b-163">Vedere gli esempi nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="ec77b-163">See examples in the next section.</span></span> |<span data-ttu-id="ec77b-164">No.</span><span class="sxs-lookup"><span data-stu-id="ec77b-164">No.</span></span> <span data-ttu-id="ec77b-165">Quando si specifica tableName senza azureTableSourceQuery, tutti i record della tabella vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="ec77b-166">Se si specifica anche azureTableSourceQuery, i record della tabella che soddisfa la query vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="ec77b-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="ec77b-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="ec77b-168">Indica se ignorare l'eccezione di tabella inesistente.</span><span class="sxs-lookup"><span data-stu-id="ec77b-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="ec77b-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="ec77b-169">TRUE</span></span><br/><span data-ttu-id="ec77b-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="ec77b-170">FALSE</span></span> |<span data-ttu-id="ec77b-171">No</span><span class="sxs-lookup"><span data-stu-id="ec77b-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="ec77b-172">esempi di azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="ec77b-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="ec77b-173">Se la colonna della tabella di Azure è di tipo stringa:</span><span class="sxs-lookup"><span data-stu-id="ec77b-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="ec77b-174">Se la colonna della tabella di Azure è di tipo datetime:</span><span class="sxs-lookup"><span data-stu-id="ec77b-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="ec77b-175">**AzureTableSink** supporta le seguenti proprietà della sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="ec77b-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="ec77b-176">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ec77b-176">Property</span></span> | <span data-ttu-id="ec77b-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ec77b-177">Description</span></span> | <span data-ttu-id="ec77b-178">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="ec77b-178">Allowed values</span></span> | <span data-ttu-id="ec77b-179">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ec77b-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec77b-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="ec77b-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="ec77b-181">Valore predefinito della chiave di partizione che può essere usato dal sink.</span><span class="sxs-lookup"><span data-stu-id="ec77b-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="ec77b-182">Valore stringa.</span><span class="sxs-lookup"><span data-stu-id="ec77b-182">A string value.</span></span> |<span data-ttu-id="ec77b-183">No</span><span class="sxs-lookup"><span data-stu-id="ec77b-183">No</span></span> |
| <span data-ttu-id="ec77b-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="ec77b-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="ec77b-185">Specificare il nome della colonna i cui valori vengono usati come chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="ec77b-186">Se non specificato, AzureTableDefaultPartitionKeyValue viene usato come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="ec77b-187">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="ec77b-187">A column name.</span></span> |<span data-ttu-id="ec77b-188">No</span><span class="sxs-lookup"><span data-stu-id="ec77b-188">No</span></span> |
| <span data-ttu-id="ec77b-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="ec77b-189">azureTableRowKeyName</span></span> |<span data-ttu-id="ec77b-190">Specificare il nome della colonna i cui valori vengono usati come chiavi di riga.</span><span class="sxs-lookup"><span data-stu-id="ec77b-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="ec77b-191">Se non specificato, usare un GUID per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="ec77b-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="ec77b-192">Nome colonna.</span><span class="sxs-lookup"><span data-stu-id="ec77b-192">A column name.</span></span> |<span data-ttu-id="ec77b-193">No</span><span class="sxs-lookup"><span data-stu-id="ec77b-193">No</span></span> |
| <span data-ttu-id="ec77b-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="ec77b-194">azureTableInsertType</span></span> |<span data-ttu-id="ec77b-195">Modalità di inserimento dei dati in una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="ec77b-196">Questa proprietà verifica se per le righe esistenti nella tabella di output con chiavi di partizione e di riga corrispondenti i valori vengono sostituiti o uniti.</span><span class="sxs-lookup"><span data-stu-id="ec77b-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="ec77b-197">Per scoprire come funzionano queste impostazioni (unione e sostituzione), vedere gli argomenti [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Inserire o unire un'entità) e [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Inserire o sostituire un'entità).</span><span class="sxs-lookup"><span data-stu-id="ec77b-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="ec77b-198">Queste impostazioni vengono applicate a livello di riga, non a livello di tabella, e nessuna delle due opzioni elimina le righe della tabella di output che non esistono nell'input.</span><span class="sxs-lookup"><span data-stu-id="ec77b-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="ec77b-199">merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="ec77b-199">merge (default)</span></span><br/><span data-ttu-id="ec77b-200">replace</span><span class="sxs-lookup"><span data-stu-id="ec77b-200">replace</span></span> |<span data-ttu-id="ec77b-201">No</span><span class="sxs-lookup"><span data-stu-id="ec77b-201">No</span></span> |
| <span data-ttu-id="ec77b-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ec77b-202">writeBatchSize</span></span> |<span data-ttu-id="ec77b-203">Inserisce dati nella tabella di Azure quando viene raggiunto il writeBatchSize o writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="ec77b-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="ec77b-204">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="ec77b-204">Integer (number of rows)</span></span> |<span data-ttu-id="ec77b-205">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="ec77b-205">No (default: 10000)</span></span> |
| <span data-ttu-id="ec77b-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ec77b-206">writeBatchTimeout</span></span> |<span data-ttu-id="ec77b-207">Inserisce i dati nella tabella di Azure quando viene raggiunto writeBatchSize o writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ec77b-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="ec77b-208">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="ec77b-208">timespan</span></span><br/><br/><span data-ttu-id="ec77b-209">Ad esempio: "00:20:00" (20 minuti)</span><span class="sxs-lookup"><span data-stu-id="ec77b-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="ec77b-210">No. (il valore predefinito è il timeout del client di archiviazione pari a 90 secondi)</span><span class="sxs-lookup"><span data-stu-id="ec77b-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="ec77b-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="ec77b-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="ec77b-212">Eseguire il mapping di una colonna di origine a una colonna di destinazione usando la funzione di conversione proprietà JSON prima di poter usare la colonna di destinazione come azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="ec77b-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="ec77b-213">Nell'esempio seguente, la colonna di origine DivisionID viene eseguito il mapping alla colonna di destinazione: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="ec77b-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="ec77b-214">DivisionID è specificato come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="ec77b-215">Esempi JSON</span><span class="sxs-lookup"><span data-stu-id="ec77b-215">JSON examples</span></span>
<span data-ttu-id="ec77b-216">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ec77b-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ec77b-217">Tali esempi mostrano come copiare dati in e dall'archivio tabelle di Azure e in e dal database BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="ec77b-218">I dati possono tuttavia essere copiati **direttamente** da qualsiasi origine a qualsiasi sink supportato.</span><span class="sxs-lookup"><span data-stu-id="ec77b-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="ec77b-219">Per altre informazioni, vedere la sezione "Archivi dati e formati supportati" in [Spostare dati con l'attività di copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ec77b-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="ec77b-220">Esempio: Copiare dati da tabelle di Azure al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ec77b-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="ec77b-221">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="ec77b-221">The following sample shows:</span></span>

1. <span data-ttu-id="ec77b-222">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).</span><span class="sxs-lookup"><span data-stu-id="ec77b-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="ec77b-223">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec77b-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="ec77b-224">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec77b-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ec77b-225">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ec77b-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ec77b-226">Nell'esempio vengono copiati i dati appartenenti alla partizione predefinita in una tabella di Azure a un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="ec77b-227">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="ec77b-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ec77b-228">**Servizio collegato di archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ec77b-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="ec77b-229">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="ec77b-230">Per il primo specificare la stringa di connessione che include la chiave dell'account e per il secondo specificare l'URI di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="ec77b-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="ec77b-231">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="ec77b-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="ec77b-232">**Set di dati di input di tabelle di Azure**</span><span class="sxs-lookup"><span data-stu-id="ec77b-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="ec77b-233">Nell'esempio si presuppone di aver creato una tabella "MyTable" in tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="ec77b-234">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="ec77b-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="ec77b-235">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ec77b-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ec77b-236">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="ec77b-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ec77b-237">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ec77b-238">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="ec77b-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="ec77b-239">**Attività di copia in una pipeline con AzureTableSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="ec77b-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="ec77b-240">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ec77b-241">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **AzureTableSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ec77b-242">La query SQL specificata con la proprietà **AzureTableSourceQuery** seleziona i dati da copiare dalla partizione predefinita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="ec77b-243">Esempio: Copiare i dati dal BLOB di Azure in tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="ec77b-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="ec77b-244">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="ec77b-244">The following sample shows:</span></span>

1. <span data-ttu-id="ec77b-245">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).</span><span class="sxs-lookup"><span data-stu-id="ec77b-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="ec77b-246">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec77b-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="ec77b-247">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec77b-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ec77b-248">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ec77b-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ec77b-249">L'esempio copia i dati di una serie temporale da un BLOB di Azure a una tabella di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="ec77b-250">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="ec77b-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ec77b-251">**Servizio collegato di Archiviazione di Azure (per tabelle di Azure e BLOB):**</span><span class="sxs-lookup"><span data-stu-id="ec77b-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="ec77b-252">Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="ec77b-253">Per il primo specificare la stringa di connessione che include la chiave dell'account e per il secondo specificare l'URI di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="ec77b-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="ec77b-254">Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="ec77b-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="ec77b-255">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ec77b-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ec77b-256">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="ec77b-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ec77b-257">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ec77b-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ec77b-258">Il percorso della cartella usa le parti anno, mese, e giorno dell'ora di inizio e il nome del file usa la parte dell'ora di inizio relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="ec77b-259">L'impostazione di "external" su "true" comunica al servizio Data Factory che il set di dati è esterno a Data Factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="ec77b-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="ec77b-260">**Set di dati di output di tabelle di Azure**</span><span class="sxs-lookup"><span data-stu-id="ec77b-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="ec77b-261">Nell’esempio vengono copiati dati in una tabella denominata "MyTable" in tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="ec77b-262">Creare una tabella di Azure con il numero di colonne atteso nel file CSV del BLOB.</span><span class="sxs-lookup"><span data-stu-id="ec77b-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="ec77b-263">Alla tabella vengono aggiunte nuove righe ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-263">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="ec77b-264">**Copiare attività in una pipeline con BlobSource e AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="ec77b-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="ec77b-265">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ec77b-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ec77b-266">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **BlobSource** e il tipo di **sink** è impostato su **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="ec77b-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="ec77b-267">Mapping dei tipi per tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="ec77b-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="ec77b-268">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipo automatiche dai tipi di origine ai tipi di sink con l'approccio in due passaggi seguente:</span><span class="sxs-lookup"><span data-stu-id="ec77b-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="ec77b-269">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="ec77b-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ec77b-270">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="ec77b-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ec77b-271">Quando si spostano i dati da e verso tabelle di Azure, i seguenti [mapping definiti dal servizio tabelle di Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) vengono usati dai tipi di OData di tabelle di Azure al tipo di .NET e viceversa.</span><span class="sxs-lookup"><span data-stu-id="ec77b-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="ec77b-272">Tipo di dati OData</span><span class="sxs-lookup"><span data-stu-id="ec77b-272">OData Data Type</span></span> | <span data-ttu-id="ec77b-273">Tipo di .NET</span><span class="sxs-lookup"><span data-stu-id="ec77b-273">.NET Type</span></span> | <span data-ttu-id="ec77b-274">Dettagli</span><span class="sxs-lookup"><span data-stu-id="ec77b-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec77b-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="ec77b-275">Edm.Binary</span></span> |<span data-ttu-id="ec77b-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="ec77b-276">byte[]</span></span> |<span data-ttu-id="ec77b-277">Una matrice di byte di dimensioni fino a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ec77b-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="ec77b-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="ec77b-278">Edm.Boolean</span></span> |<span data-ttu-id="ec77b-279">bool</span><span class="sxs-lookup"><span data-stu-id="ec77b-279">bool</span></span> |<span data-ttu-id="ec77b-280">Valore booleano.</span><span class="sxs-lookup"><span data-stu-id="ec77b-280">A Boolean value.</span></span> |
| <span data-ttu-id="ec77b-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="ec77b-281">Edm.DateTime</span></span> |<span data-ttu-id="ec77b-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="ec77b-282">DateTime</span></span> |<span data-ttu-id="ec77b-283">Un valore a 64 bit espresso come Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="ec77b-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="ec77b-284">L'intervallo DateTime supportato inizia dalle 00:00, 1 gennaio, 1601 D.C.</span><span class="sxs-lookup"><span data-stu-id="ec77b-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="ec77b-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="ec77b-285">(C.E.), UTC.</span></span> <span data-ttu-id="ec77b-286">L'intervallo termina il 31 dicembre 9999.</span><span class="sxs-lookup"><span data-stu-id="ec77b-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="ec77b-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="ec77b-287">Edm.Double</span></span> |<span data-ttu-id="ec77b-288">double</span><span class="sxs-lookup"><span data-stu-id="ec77b-288">double</span></span> |<span data-ttu-id="ec77b-289">Un valore a virgola mobile a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="ec77b-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="ec77b-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="ec77b-290">Edm.Guid</span></span> |<span data-ttu-id="ec77b-291">Guid</span><span class="sxs-lookup"><span data-stu-id="ec77b-291">Guid</span></span> |<span data-ttu-id="ec77b-292">Un identificatore univoco globale a 128 bit.</span><span class="sxs-lookup"><span data-stu-id="ec77b-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="ec77b-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="ec77b-293">Edm.Int32</span></span> |<span data-ttu-id="ec77b-294">Int32</span><span class="sxs-lookup"><span data-stu-id="ec77b-294">Int32</span></span> |<span data-ttu-id="ec77b-295">Un valore integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="ec77b-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="ec77b-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="ec77b-296">Edm.Int64</span></span> |<span data-ttu-id="ec77b-297">Int64</span><span class="sxs-lookup"><span data-stu-id="ec77b-297">Int64</span></span> |<span data-ttu-id="ec77b-298">Un valore integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="ec77b-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="ec77b-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="ec77b-299">Edm.String</span></span> |<span data-ttu-id="ec77b-300">String</span><span class="sxs-lookup"><span data-stu-id="ec77b-300">String</span></span> |<span data-ttu-id="ec77b-301">Un valore con codifica UTF-16.</span><span class="sxs-lookup"><span data-stu-id="ec77b-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="ec77b-302">I valori delle stringhe possono essere di dimensioni fino a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ec77b-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="ec77b-303">Esempio di conversione di tipo</span><span class="sxs-lookup"><span data-stu-id="ec77b-303">Type Conversion Sample</span></span>
<span data-ttu-id="ec77b-304">L'esempio seguente riguarda la copia dei dati da un BLOB di Azure a tabelle di Azure con conversioni del tipo.</span><span class="sxs-lookup"><span data-stu-id="ec77b-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="ec77b-305">Si supponga che il set di dati BLOB sia in formato CSV e contenga tre colonne.</span><span class="sxs-lookup"><span data-stu-id="ec77b-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="ec77b-306">Una di esse è una colonna datetime con un formato datetime personalizzato che utilizza nomi abbreviati francesi per il giorno della settimana.</span><span class="sxs-lookup"><span data-stu-id="ec77b-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="ec77b-307">Definire il set di dati di origine BLOB come indicato di seguito e le definizioni di tipo per le colonne.</span><span class="sxs-lookup"><span data-stu-id="ec77b-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

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
<span data-ttu-id="ec77b-308">Dato il precedente mapping dei tipi dal tipo OData di tabelle di Azure al tipo di .NET è possibile definire la tabella in tabelle di Azure con lo schema seguente.</span><span class="sxs-lookup"><span data-stu-id="ec77b-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="ec77b-309">**Schema di tabelle di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ec77b-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="ec77b-310">Nome colonna</span><span class="sxs-lookup"><span data-stu-id="ec77b-310">Column name</span></span> | <span data-ttu-id="ec77b-311">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec77b-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="ec77b-312">userid</span><span class="sxs-lookup"><span data-stu-id="ec77b-312">userid</span></span> |<span data-ttu-id="ec77b-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="ec77b-313">Edm.Int64</span></span> |
| <span data-ttu-id="ec77b-314">name</span><span class="sxs-lookup"><span data-stu-id="ec77b-314">name</span></span> |<span data-ttu-id="ec77b-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="ec77b-315">Edm.String</span></span> |
| <span data-ttu-id="ec77b-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="ec77b-316">lastlogindate</span></span> |<span data-ttu-id="ec77b-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="ec77b-317">Edm.DateTime</span></span> |

<span data-ttu-id="ec77b-318">Quindi si definisce il set di dati di tabelle di Azure come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ec77b-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="ec77b-319">Non è necessario specificare la sezione "struttura" con informazioni sul tipo perché le informazioni sul tipo sono già state specificate nell'archivio dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="ec77b-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

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

<span data-ttu-id="ec77b-320">In questo caso Data Factory esegue automaticamente la conversione del tipo incluso il campo Datetime con il formato data personalizzato usando "fr-fr" quando si spostano dati da BLOB a tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="ec77b-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="ec77b-321">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ec77b-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ec77b-322">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="ec77b-322">Performance and Tuning</span></span>
<span data-ttu-id="ec77b-323">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="ec77b-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
