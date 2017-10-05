---
title: Spostare dati da e verso Azure Cosmos DB | Microsoft Docs
description: Informazioni su come spostare i dati da e verso la raccolta di Azure Cosmos DB mediante Azure Data Factory
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="c8529-103">Spostare dati da e verso il BLOB di Azure mediante Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="c8529-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="c8529-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso Azure Cosmos DB (API DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="c8529-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="c8529-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="c8529-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="c8529-106">È possibile copiare i dati da qualsiasi archivio dati di origine supportato ad Azure Cosmos DB o da Azure Cosmos DB a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="c8529-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="c8529-107">Per un elenco degli archivi dati supportati come origini o sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c8529-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c8529-108">Il connettore Azure Cosmos DB supporta solo l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c8529-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="c8529-109">Per copiare i dati così come sono da e verso i file JSON o un'altra raccolta Cosmos DB, vedere [Importare/esportare documenti JSON](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="c8529-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c8529-110">introduttiva</span><span class="sxs-lookup"><span data-stu-id="c8529-110">Getting started</span></span>
<span data-ttu-id="c8529-111">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso Azure Cosmos DB usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="c8529-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="c8529-112">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="c8529-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c8529-113">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="c8529-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="c8529-114">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="c8529-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c8529-115">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="c8529-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c8529-116">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="c8529-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="c8529-117">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c8529-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c8529-118">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="c8529-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c8529-119">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="c8529-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c8529-120">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c8529-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c8529-121">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="c8529-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c8529-122">Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso Cosmos DB, vedere la sezione degli [esempi JSON](#json-examples) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c8529-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="c8529-123">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di Data factory specifiche di Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="c8529-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="c8529-124">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="c8529-124">Linked service properties</span></span>
<span data-ttu-id="c8529-125">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="c8529-126">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="c8529-126">**Property**</span></span> | <span data-ttu-id="c8529-127">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c8529-127">**Description**</span></span> | <span data-ttu-id="c8529-128">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="c8529-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8529-129">type</span><span class="sxs-lookup"><span data-stu-id="c8529-129">type</span></span> |<span data-ttu-id="c8529-130">La proprietà del tipo deve essere impostata su: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="c8529-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="c8529-131">Sì</span><span class="sxs-lookup"><span data-stu-id="c8529-131">Yes</span></span> |
| <span data-ttu-id="c8529-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="c8529-132">connectionString</span></span> |<span data-ttu-id="c8529-133">Specificare le informazioni necessarie per connettersi al database di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="c8529-134">Sì</span><span class="sxs-lookup"><span data-stu-id="c8529-134">Yes</span></span> |

<span data-ttu-id="c8529-135">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c8529-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c8529-136">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="c8529-136">Dataset properties</span></span>
<span data-ttu-id="c8529-137">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, fare riferimento all'articolo [Creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c8529-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c8529-138">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="c8529-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c8529-139">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="c8529-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c8529-140">La sezione typeProperties per il set di dati di tipo **DocumentDbCollection** presenta le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="c8529-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="c8529-141">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="c8529-141">**Property**</span></span> | <span data-ttu-id="c8529-142">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c8529-142">**Description**</span></span> | <span data-ttu-id="c8529-143">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="c8529-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8529-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="c8529-144">collectionName</span></span> |<span data-ttu-id="c8529-145">Nome della raccolta documenti di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="c8529-146">Sì</span><span class="sxs-lookup"><span data-stu-id="c8529-146">Yes</span></span> |

<span data-ttu-id="c8529-147">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c8529-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="c8529-148">Schema da Data Factory</span><span class="sxs-lookup"><span data-stu-id="c8529-148">Schema by Data Factory</span></span>
<span data-ttu-id="c8529-149">Per gli archivi di dati privi di schema, ad esempio Azure Cosmos DB, il servizio Data Factory deduce lo schema in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8529-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="c8529-150">Se si specifica la struttura dei dati tramite la proprietà **structure** nella definizione del set di dati, il servizio Data Factory considera la struttura come schema.</span><span class="sxs-lookup"><span data-stu-id="c8529-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="c8529-151">In questo caso, se una riga non contiene un valore per una colonna, verrà inserito un valore null.</span><span class="sxs-lookup"><span data-stu-id="c8529-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="c8529-152">Se non si specifica la struttura dei dati usando la proprietà **structure** nella definizione del set di dati, il servizio Data Factory deduce lo schema usando la prima riga di dati.</span><span class="sxs-lookup"><span data-stu-id="c8529-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="c8529-153">In questo caso, se la prima riga non contiene lo schema completo, alcune colonne non saranno presenti nel risultato dell'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="c8529-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="c8529-154">Di conseguenza, per le origini dati prive di schema, la procedura consigliata consiste nello specificare la struttura dei dati usando la proprietà **structure** .</span><span class="sxs-lookup"><span data-stu-id="c8529-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c8529-155">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="c8529-155">Copy activity properties</span></span>
<span data-ttu-id="c8529-156">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c8529-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c8529-157">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="c8529-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="c8529-158">L'attività di copia accetta solo un input e produce solo un output.</span><span class="sxs-lookup"><span data-stu-id="c8529-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="c8529-159">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece per ogni tipo di attività e in caso di attività di copia variano in base ai tipi di origini e ai sink.</span><span class="sxs-lookup"><span data-stu-id="c8529-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c8529-160">In caso di attività di copia con origine di tipo **DocumentDbCollectionSource**, sono disponibili le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="c8529-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="c8529-161">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="c8529-161">**Property**</span></span> | <span data-ttu-id="c8529-162">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c8529-162">**Description**</span></span> | <span data-ttu-id="c8529-163">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="c8529-163">**Allowed values**</span></span> | <span data-ttu-id="c8529-164">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="c8529-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c8529-165">query</span><span class="sxs-lookup"><span data-stu-id="c8529-165">query</span></span> |<span data-ttu-id="c8529-166">Specificare la query per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="c8529-166">Specify the query to read data.</span></span> |<span data-ttu-id="c8529-167">Stringa di query supportata da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="c8529-168">Esempio: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="c8529-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="c8529-169">No</span><span class="sxs-lookup"><span data-stu-id="c8529-169">No</span></span> <br/><br/><span data-ttu-id="c8529-170">Se non specificato, l'istruzione SQL eseguita: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="c8529-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="c8529-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="c8529-171">nestingSeparator</span></span> |<span data-ttu-id="c8529-172">Carattere speciale per indicare che il documento è nidificato</span><span class="sxs-lookup"><span data-stu-id="c8529-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="c8529-173">Qualsiasi carattere.</span><span class="sxs-lookup"><span data-stu-id="c8529-173">Any character.</span></span> <br/><br/><span data-ttu-id="c8529-174">Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate.</span><span class="sxs-lookup"><span data-stu-id="c8529-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="c8529-175">Azure Data Factory consente di indicare una gerarchia tramite nestingSeparator, ovvero "."</span><span class="sxs-lookup"><span data-stu-id="c8529-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="c8529-176">negli esempi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c8529-176">in the above examples.</span></span> <span data-ttu-id="c8529-177">Con il separatore, l'attività copia genererà l'oggetto "Name" con tre elementi figlio First, Middle e Last, in base a "Name.First", "Name.Middle" e "Name.Last" nella definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="c8529-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="c8529-178">No</span><span class="sxs-lookup"><span data-stu-id="c8529-178">No</span></span> |

<span data-ttu-id="c8529-179">**DocumentDbCollectionSink** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8529-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="c8529-180">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="c8529-180">**Property**</span></span> | <span data-ttu-id="c8529-181">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c8529-181">**Description**</span></span> | <span data-ttu-id="c8529-182">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="c8529-182">**Allowed values**</span></span> | <span data-ttu-id="c8529-183">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="c8529-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c8529-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="c8529-184">nestingSeparator</span></span> |<span data-ttu-id="c8529-185">È necessario un carattere speciale nel nome della colonna di origine per indicare tale documento nidificato.</span><span class="sxs-lookup"><span data-stu-id="c8529-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="c8529-186">Per l'esempio sopra: `Name.First` nella tabella di output produce la struttura JSON seguente nel documento di Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="c8529-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="c8529-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="c8529-187">"Name": {</span></span><br/>    <span data-ttu-id="c8529-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="c8529-188">"First": "John"</span></span><br/><span data-ttu-id="c8529-189">},</span><span class="sxs-lookup"><span data-stu-id="c8529-189">},</span></span> |<span data-ttu-id="c8529-190">Carattere utilizzato per separare i livelli di nidificazione.</span><span class="sxs-lookup"><span data-stu-id="c8529-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="c8529-191">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="c8529-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="c8529-192">Carattere utilizzato per separare i livelli di nidificazione.</span><span class="sxs-lookup"><span data-stu-id="c8529-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="c8529-193">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="c8529-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="c8529-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="c8529-194">writeBatchSize</span></span> |<span data-ttu-id="c8529-195">Numero di richieste in parallelo per il servizio Azure Cosmos DB per creare documenti.</span><span class="sxs-lookup"><span data-stu-id="c8529-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="c8529-196">È possibile ottimizzare le prestazioni quando si copiano dati da e verso Cosmos DB usando questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="c8529-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="c8529-197">È possibile prevedere prestazioni migliori quando si aumenta writeBatchSize, poiché vengono inviate più richieste in parallelo a Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="c8529-198">Tuttavia è necessario evitare la limitazione che può generare il messaggio di errore: "La frequenza delle richieste è troppo elevata".</span><span class="sxs-lookup"><span data-stu-id="c8529-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="c8529-199">La limitazione è dovuta a diversi fattori, inclusi la dimensione dei documenti, il numero di termini nei documenti, i criteri di indicizzazione della raccolta di destinazione, ecc. Per le operazioni di copia, è possibile usare una raccolta migliore, ad esempio S3, per disporre della massima velocità effettiva disponibile, ovvero 2500 unità di richiesta al secondo.</span><span class="sxs-lookup"><span data-stu-id="c8529-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="c8529-200">Integer</span><span class="sxs-lookup"><span data-stu-id="c8529-200">Integer</span></span> |<span data-ttu-id="c8529-201">No (valore predefinito: 5)</span><span class="sxs-lookup"><span data-stu-id="c8529-201">No (default: 5)</span></span> |
| <span data-ttu-id="c8529-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="c8529-202">writeBatchTimeout</span></span> |<span data-ttu-id="c8529-203">Tempo di attesa per il completamento dell’operazione prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="c8529-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="c8529-204">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="c8529-204">timespan</span></span><br/><br/> <span data-ttu-id="c8529-205">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="c8529-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="c8529-206">No</span><span class="sxs-lookup"><span data-stu-id="c8529-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="c8529-207">Importare/esportare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="c8529-207">Import/Export JSON documents</span></span>
<span data-ttu-id="c8529-208">Usando questo connettore Cosmos DB, è possibile:</span><span class="sxs-lookup"><span data-stu-id="c8529-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="c8529-209">Importare i documenti JSON da diverse origini in Cosmos DB, tra cui BLOB di Azure, Azure Data Lake, file system locale o altri archivi di file supportati da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8529-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="c8529-210">Esportare i documenti JSON da raccolte Cosmos DB in diversi archivi basati su file.</span><span class="sxs-lookup"><span data-stu-id="c8529-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="c8529-211">Eseguire la migrazione dei dati tra due raccolte Cosmos DB così come sono.</span><span class="sxs-lookup"><span data-stu-id="c8529-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="c8529-212">Per ottenere la copia senza schema,</span><span class="sxs-lookup"><span data-stu-id="c8529-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="c8529-213">Quando si usa la copia guidata, controllare l'opzione **"Export as-is to JSON files or Cosmos DB collection"** (Esportare così come sono nel file JSON o in una raccolta di Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="c8529-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="c8529-214">Quando si usa la modifica JSON, non specificare la sezione "struttura" nel set di dati di Cosmos DB o né la proprietà "nestingSeparator" nell'origine/sink di Cosmos DB nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="c8529-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="c8529-215">Per importare/esportare verso i file JSON, nel set di dati dell'archivio file specificare il tipo di formato come "JsonFormat", la configurazione come "filePattern" e ignorare le altre impostazioni del formato, vedere la sezione [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c8529-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="c8529-216">Esempi JSON</span><span class="sxs-lookup"><span data-stu-id="c8529-216">JSON examples</span></span>
<span data-ttu-id="c8529-217">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c8529-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c8529-218">Tali esempi mostrano come copiare dati da e verso Azure Cosmos DB e Archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8529-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="c8529-219">I dati possono anche essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8529-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="c8529-220">Esempio: Copiare dati da Azure Cosmos DB a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c8529-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="c8529-221">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="c8529-221">The sample below shows:</span></span>

1. <span data-ttu-id="c8529-222">Un servizio collegato di tipo [DocumentDB](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="c8529-223">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c8529-224">Un [set di dati](data-factory-create-datasets.md) di input di tipo [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="c8529-225">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c8529-226">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c8529-227">L'esempio copia dati da Azure Cosmos DB a BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8529-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="c8529-228">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="c8529-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c8529-229">**Servizio collegato di Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="c8529-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="c8529-230">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="c8529-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="c8529-231">**Set di dati di input di Azure DocumentDB:**</span><span class="sxs-lookup"><span data-stu-id="c8529-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="c8529-232">L'esempio presuppone che sia presente una raccolta denominata **Person** in un database di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="c8529-233">Impostando "external" su "true" e specificando i criteri externalData si comunica al servizio Data factory di Azure che la tabella è esterna e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="c8529-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="c8529-234">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="c8529-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c8529-235">I dati vengono copiati in un nuovo BLOB ogni ora e il percorso del BLOB riflette la data e l'ora specifiche con granularità oraria.</span><span class="sxs-lookup"><span data-stu-id="c8529-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c8529-236">Documento JSON di esempio nella raccolta Person in un database di Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="c8529-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="c8529-237">Cosmos DB supporta l’esecuzione di query di documenti utilizzando una sintassi come SQL su documenti JSON gerarchici.</span><span class="sxs-lookup"><span data-stu-id="c8529-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="c8529-238">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c8529-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="c8529-239">La pipeline seguente copia i dati dalla raccolta Person nel database di Azure Cosmos DB a un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8529-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="c8529-240">Come parte dell'attività di copia, i set di dati di input e output sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="c8529-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="c8529-241">Esempio: Copiare dati da BLOB di Azure ad Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8529-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="c8529-242">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="c8529-242">The sample below shows:</span></span>

1. <span data-ttu-id="c8529-243">Un servizio collegato di tipo [DocumentDB](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="c8529-244">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c8529-245">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="c8529-246">Un [set di dati](data-factory-create-datasets.md) di output di tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="c8529-247">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="c8529-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="c8529-248">L'esempio copia dati da BLOB di Azure ad Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="c8529-249">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="c8529-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c8529-250">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="c8529-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="c8529-251">**Servizio collegato di Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="c8529-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="c8529-252">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="c8529-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c8529-253">**Set di dati di output di Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="c8529-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="c8529-254">Nell'esempio vengono copiati dati a una raccolta denominata "Person".</span><span class="sxs-lookup"><span data-stu-id="c8529-254">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c8529-255">La pipeline seguente copia i dati dal BLOB di Azure alla raccolta Person in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8529-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="c8529-256">Come parte dell'attività di copia, i set di dati di input e output sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="c8529-256">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="c8529-257">Se l’input BLOB d’esempio è come</span><span class="sxs-lookup"><span data-stu-id="c8529-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="c8529-258">Quindi l'output JSON in Cosmos DB sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="c8529-258">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="c8529-259">Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate.</span><span class="sxs-lookup"><span data-stu-id="c8529-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="c8529-260">Azure Data Factory consente di indicare una gerarchia tramite **nestingSeparator**, ovvero "."</span><span class="sxs-lookup"><span data-stu-id="c8529-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="c8529-261">in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="c8529-261">in this example.</span></span> <span data-ttu-id="c8529-262">Con il separatore, l'attività copia genererà l'oggetto "Name" con tre elementi figlio First, Middle e Last, in base a "Name.First", "Name.Middle" e "Name.Last" nella definizione della tabella.</span><span class="sxs-lookup"><span data-stu-id="c8529-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="c8529-263">Appendice</span><span class="sxs-lookup"><span data-stu-id="c8529-263">Appendix</span></span>
1. <span data-ttu-id="c8529-264">**Domanda:** C’è l'aggiornamento del supporto di attività di copia dei record esistenti?</span><span class="sxs-lookup"><span data-stu-id="c8529-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="c8529-265">**Risposta:** No.</span><span class="sxs-lookup"><span data-stu-id="c8529-265">**Answer:** No.</span></span>
2. <span data-ttu-id="c8529-266">**Domanda:** funzionamento un nuovo tentativo di una copia di database Cosmos Azure gestiscono già copiati i record?</span><span class="sxs-lookup"><span data-stu-id="c8529-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="c8529-267">**Risposta:** se i record dispongono di un campo "ID" e l'operazione di copia tenta di inserire un record con lo stesso ID, l'operazione di copia genera un errore.</span><span class="sxs-lookup"><span data-stu-id="c8529-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="c8529-268">**Domanda:** Data Factory supporta [intervallo o il partizionamento dei dati basati su hash](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="c8529-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="c8529-269">**Risposta:** No.</span><span class="sxs-lookup"><span data-stu-id="c8529-269">**Answer:** No.</span></span>
4. <span data-ttu-id="c8529-270">**Domanda:** è possibile specificare più di una raccolta di Azure Cosmos DB per una tabella?</span><span class="sxs-lookup"><span data-stu-id="c8529-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="c8529-271">**Risposta:** No.</span><span class="sxs-lookup"><span data-stu-id="c8529-271">**Answer:** No.</span></span> <span data-ttu-id="c8529-272">In questo momento, è possibile specificare solo una raccolta.</span><span class="sxs-lookup"><span data-stu-id="c8529-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c8529-273">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c8529-273">Performance and Tuning</span></span>
<span data-ttu-id="c8529-274">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c8529-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
