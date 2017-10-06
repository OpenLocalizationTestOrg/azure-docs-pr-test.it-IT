---
title: aaaMove dati da e verso Azure Cosmos DB | Documenti Microsoft
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
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="ccf41-103">Spostare dati tooand da DB Cosmos Azure usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ccf41-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="ccf41-104">Questo articolo spiega come toouse hello attività di copia nei dati toomove Azure Data Factory di Azure Cosmos DB (API DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="ccf41-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="ccf41-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="ccf41-106">È possibile copiare dati da qualsiasi origine supportati dati archiviano tooAzure DB Cosmos o dai dati di Azure Cosmos DB tooany supportati sink archiviano.</span><span class="sxs-lookup"><span data-stu-id="ccf41-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="ccf41-107">Per un elenco di archivi dati come origini o sink è supportato dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="ccf41-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ccf41-108">Il connettore Azure Cosmos DB supporta solo l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ccf41-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="ccf41-109">dati toocopy come-è a/da file JSON o un'altra raccolta Cosmos DB, vedere [documenti JSON di importazione/esportazione](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="ccf41-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="ccf41-110">introduttiva</span><span class="sxs-lookup"><span data-stu-id="ccf41-110">Getting started</span></span>
<span data-ttu-id="ccf41-111">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso Azure Cosmos DB usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="ccf41-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="ccf41-112">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="ccf41-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ccf41-113">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="ccf41-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ccf41-114">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="ccf41-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ccf41-115">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ccf41-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ccf41-116">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccf41-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ccf41-117">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="ccf41-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ccf41-118">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ccf41-119">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="ccf41-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ccf41-120">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ccf41-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ccf41-121">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ccf41-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ccf41-122">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati dati da e verso Cosmos DB, vedere [esempi JSON](#json-examples) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ccf41-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="ccf41-123">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooCosmos DB:</span><span class="sxs-lookup"><span data-stu-id="ccf41-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ccf41-124">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="ccf41-124">Linked service properties</span></span>
<span data-ttu-id="ccf41-125">Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooAzure servizio DB Cosmos collegato.</span><span class="sxs-lookup"><span data-stu-id="ccf41-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="ccf41-126">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="ccf41-126">**Property**</span></span> | <span data-ttu-id="ccf41-127">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ccf41-127">**Description**</span></span> | <span data-ttu-id="ccf41-128">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="ccf41-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccf41-129">type</span><span class="sxs-lookup"><span data-stu-id="ccf41-129">type</span></span> |<span data-ttu-id="ccf41-130">proprietà di tipo Hello deve essere impostata su: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="ccf41-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="ccf41-131">Sì</span><span class="sxs-lookup"><span data-stu-id="ccf41-131">Yes</span></span> |
| <span data-ttu-id="ccf41-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="ccf41-132">connectionString</span></span> |<span data-ttu-id="ccf41-133">Specificare le informazioni necessarie tooconnect tooAzure DB Cosmos database.</span><span class="sxs-lookup"><span data-stu-id="ccf41-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="ccf41-134">Sì</span><span class="sxs-lookup"><span data-stu-id="ccf41-134">Yes</span></span> |

<span data-ttu-id="ccf41-135">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ccf41-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="ccf41-136">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="ccf41-136">Dataset properties</span></span>
<span data-ttu-id="ccf41-137">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere toohello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ccf41-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ccf41-138">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="ccf41-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ccf41-139">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ccf41-140">Hello typeProperties sezione hello set di dati di tipo **DocumentDbCollection** è hello le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="ccf41-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="ccf41-141">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="ccf41-141">**Property**</span></span> | <span data-ttu-id="ccf41-142">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ccf41-142">**Description**</span></span> | <span data-ttu-id="ccf41-143">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="ccf41-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccf41-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="ccf41-144">collectionName</span></span> |<span data-ttu-id="ccf41-145">Nome della raccolta documenti Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="ccf41-146">Sì</span><span class="sxs-lookup"><span data-stu-id="ccf41-146">Yes</span></span> |

<span data-ttu-id="ccf41-147">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ccf41-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="ccf41-148">Schema da Data Factory</span><span class="sxs-lookup"><span data-stu-id="ccf41-148">Schema by Data Factory</span></span>
<span data-ttu-id="ccf41-149">Per gli archivi dati privi di schema, ad esempio Azure Cosmos DB hello servizio Data Factory di inferenza dello schema di hello in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="ccf41-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="ccf41-150">Se si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, hello servizio Data Factory rispetta questa struttura come schema hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="ccf41-151">In questo caso, se una riga non contiene un valore per una colonna, verrà inserito un valore null.</span><span class="sxs-lookup"><span data-stu-id="ccf41-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="ccf41-152">Se non si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, hello servizio Data Factory di inferenza dello schema di hello utilizzando prima riga hello nei dati hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="ccf41-153">In questo caso, se hello prima riga contiene schema completo hello, alcune colonne sarà presente nel risultato hello dell'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="ccf41-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="ccf41-154">Pertanto, per le origini dati privi di schema consigliata hello è struttura hello toospecify dei dati tramite hello **struttura** proprietà.</span><span class="sxs-lookup"><span data-stu-id="ccf41-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="ccf41-155">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="ccf41-155">Copy activity properties</span></span>
<span data-ttu-id="ccf41-156">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere toohello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ccf41-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ccf41-157">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="ccf41-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ccf41-158">Hello attività di copia accetta un solo input e produce un solo output.</span><span class="sxs-lookup"><span data-stu-id="ccf41-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ccf41-159">Le proprietà disponibili nella sezione typeProperties hello di attività hello hello invece variano con ogni tipo di attività e in caso di attività di copia variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="ccf41-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ccf41-160">In caso di attività di copia, l'origine è di tipo **DocumentDbCollectionSource** hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="ccf41-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ccf41-161">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="ccf41-161">**Property**</span></span> | <span data-ttu-id="ccf41-162">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ccf41-162">**Description**</span></span> | <span data-ttu-id="ccf41-163">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="ccf41-163">**Allowed values**</span></span> | <span data-ttu-id="ccf41-164">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="ccf41-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ccf41-165">query</span><span class="sxs-lookup"><span data-stu-id="ccf41-165">query</span></span> |<span data-ttu-id="ccf41-166">Specificare i dati di tooread query hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="ccf41-167">Stringa di query supportata da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccf41-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="ccf41-168">Esempio: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="ccf41-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="ccf41-169">No</span><span class="sxs-lookup"><span data-stu-id="ccf41-169">No</span></span> <br/><br/><span data-ttu-id="ccf41-170">Se non specificato, hello istruzione SQL eseguita:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="ccf41-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="ccf41-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="ccf41-171">nestingSeparator</span></span> |<span data-ttu-id="ccf41-172">Carattere speciale tooindicate che hello documento nidificato</span><span class="sxs-lookup"><span data-stu-id="ccf41-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="ccf41-173">Qualsiasi carattere.</span><span class="sxs-lookup"><span data-stu-id="ccf41-173">Any character.</span></span> <br/><br/><span data-ttu-id="ccf41-174">Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate.</span><span class="sxs-lookup"><span data-stu-id="ccf41-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="ccf41-175">Data Factory di Azure consente gerarchia toodenote utente tramite nestingSeparator, ovvero "."</span><span class="sxs-lookup"><span data-stu-id="ccf41-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="ccf41-176">in hello esempi sopra riportati.</span><span class="sxs-lookup"><span data-stu-id="ccf41-176">in hello above examples.</span></span> <span data-ttu-id="ccf41-177">Con il separatore di hello, attività di copia hello genererà l'oggetto "Name" hello con elementi tre figli prima, intermedio e ultimo, in base too"Name.First", "Name.Middle" e "." in hello "Cognome" definizione di tabella.</span><span class="sxs-lookup"><span data-stu-id="ccf41-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="ccf41-178">No</span><span class="sxs-lookup"><span data-stu-id="ccf41-178">No</span></span> |

<span data-ttu-id="ccf41-179">**DocumentDbCollectionSink** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccf41-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="ccf41-180">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="ccf41-180">**Property**</span></span> | <span data-ttu-id="ccf41-181">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ccf41-181">**Description**</span></span> | <span data-ttu-id="ccf41-182">**Valori consentiti**</span><span class="sxs-lookup"><span data-stu-id="ccf41-182">**Allowed values**</span></span> | <span data-ttu-id="ccf41-183">**Obbligatorio**</span><span class="sxs-lookup"><span data-stu-id="ccf41-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ccf41-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="ccf41-184">nestingSeparator</span></span> |<span data-ttu-id="ccf41-185">È necessario un carattere speciale nel hello origine colonna nome tooindicate annidati di documento.</span><span class="sxs-lookup"><span data-stu-id="ccf41-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="ccf41-186">Ad esempio sopra: `Name.First` nell'output di hello tabella produce hello seguente struttura JSON nel documento Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="ccf41-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="ccf41-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="ccf41-187">"Name": {</span></span><br/>    <span data-ttu-id="ccf41-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="ccf41-188">"First": "John"</span></span><br/><span data-ttu-id="ccf41-189">},</span><span class="sxs-lookup"><span data-stu-id="ccf41-189">},</span></span> |<span data-ttu-id="ccf41-190">Carattere usato tooseparate livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="ccf41-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="ccf41-191">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="ccf41-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="ccf41-192">Carattere usato tooseparate livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="ccf41-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="ccf41-193">Il valore predefinito è `.` (punto).</span><span class="sxs-lookup"><span data-stu-id="ccf41-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="ccf41-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ccf41-194">writeBatchSize</span></span> |<span data-ttu-id="ccf41-195">Numero parallelo di richieste di documenti di toocreate tooAzure DB Cosmos del servizio.</span><span class="sxs-lookup"><span data-stu-id="ccf41-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="ccf41-196">È possibile ottimizzare le prestazioni di hello quando si copiano dati da e verso Cosmos DB usando questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="ccf41-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="ccf41-197">È possibile prevedere prestazioni migliori quando si aumenta viene raggiunto writeBatchSize poiché vengono inviate altre richieste in parallelo tooCosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccf41-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="ccf41-198">Tuttavia, occorre tooavoid la limitazione delle richieste che possono generare il messaggio di errore hello: "Richiesta frequenza è grande".</span><span class="sxs-lookup"><span data-stu-id="ccf41-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="ccf41-199">La limitazione è dovuta a diversi fattori, inclusi la dimensione dei documenti, il numero di termini nei documenti, i criteri di indicizzazione della raccolta di destinazione, ecc. Per le operazioni di copia, è possibile utilizzare un migliore hello toohave raccolta (ad esempio S3) la maggior parte delle velocità effettiva disponibile (2.500 richiesta unità al secondo).</span><span class="sxs-lookup"><span data-stu-id="ccf41-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="ccf41-200">Integer</span><span class="sxs-lookup"><span data-stu-id="ccf41-200">Integer</span></span> |<span data-ttu-id="ccf41-201">No (valore predefinito: 5)</span><span class="sxs-lookup"><span data-stu-id="ccf41-201">No (default: 5)</span></span> |
| <span data-ttu-id="ccf41-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ccf41-202">writeBatchTimeout</span></span> |<span data-ttu-id="ccf41-203">Tempo di attesa per hello operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="ccf41-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="ccf41-204">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="ccf41-204">timespan</span></span><br/><br/> <span data-ttu-id="ccf41-205">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="ccf41-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ccf41-206">No</span><span class="sxs-lookup"><span data-stu-id="ccf41-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="ccf41-207">Importare/esportare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="ccf41-207">Import/Export JSON documents</span></span>
<span data-ttu-id="ccf41-208">Usando questo connettore Cosmos DB, è possibile:</span><span class="sxs-lookup"><span data-stu-id="ccf41-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="ccf41-209">Importare i documenti JSON da diverse origini in Cosmos DB, tra cui BLOB di Azure, Azure Data Lake, file system locale o altri archivi di file supportati da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ccf41-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="ccf41-210">Esportare i documenti JSON da raccolte Cosmos DB in diversi archivi basati su file.</span><span class="sxs-lookup"><span data-stu-id="ccf41-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="ccf41-211">Eseguire la migrazione dei dati tra due raccolte Cosmos DB così come sono.</span><span class="sxs-lookup"><span data-stu-id="ccf41-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="ccf41-212">tooachieve copiare tale schema indipendente,</span><span class="sxs-lookup"><span data-stu-id="ccf41-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="ccf41-213">Quando si utilizza Copia guidata, selezionare hello **"esportazione-è tooJSON file o una raccolta di Cosmos DB"** opzione.</span><span class="sxs-lookup"><span data-stu-id="ccf41-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="ccf41-214">Quando utilizzare la funzione JSON, non si specifica sezione "struttura" hello in set di dati DB Cosmos né "nestingSeparator" proprietà Cosmos DB origine/sink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ccf41-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="ccf41-215">tooimport da / tooJSON file di esportazione, nel set di dati archivio file hello specificare il tipo di formato come "JsonFormat", "filePattern" configurazione e ignorare le impostazioni del formato di hello rest, vedere [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) sezione sui dettagli.</span><span class="sxs-lookup"><span data-stu-id="ccf41-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="ccf41-216">Esempi JSON</span><span class="sxs-lookup"><span data-stu-id="ccf41-216">JSON examples</span></span>
<span data-ttu-id="ccf41-217">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ccf41-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ccf41-218">Vengono visualizzate come toocopy tooand di dati da database Cosmos di Azure e archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf41-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="ccf41-219">Tuttavia, i dati possono essere copiati **direttamente** da qualsiasi hello origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ccf41-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="ccf41-220">Esempio: Copiare i dati da Azure Cosmos DB tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="ccf41-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="ccf41-221">viene illustrato l'esempio Hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ccf41-221">hello sample below shows:</span></span>

1. <span data-ttu-id="ccf41-222">Un servizio collegato di tipo [DocumentDB](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="ccf41-223">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ccf41-224">Un [set di dati](data-factory-create-datasets.md) di input di tipo [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="ccf41-225">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ccf41-226">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ccf41-227">esempio Hello copia di dati in Azure Cosmos DB tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="ccf41-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="ccf41-228">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ccf41-229">**Servizio collegato di Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="ccf41-230">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ccf41-231">**Set di dati di input di Azure DocumentDB:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="ccf41-232">esempio Hello presuppone di disporre di una raccolta denominata **persona** in un database di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccf41-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="ccf41-233">L'impostazione "external": "true" e specificando externalData informazioni sui criteri del servizio tabella hello hello Azure Data Factory è data factory di toohello esterni e non prodotte da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="ccf41-234">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ccf41-235">Dati viene copiato tooa nuovo blob ogni ora con il percorso di hello per blob hello Reflection hello specifico datetime con granularità oraria.</span><span class="sxs-lookup"><span data-stu-id="ccf41-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="ccf41-236">Documento JSON di esempio nella raccolta di persona in un database DB Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="ccf41-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="ccf41-237">Cosmos DB supporta l’esecuzione di query di documenti utilizzando una sintassi come SQL su documenti JSON gerarchici.</span><span class="sxs-lookup"><span data-stu-id="ccf41-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="ccf41-238">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ccf41-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="ccf41-239">esempio Hello pipeline copia i dati da hello raccolta persona in hello Azure Cosmos DB database tooan blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf41-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="ccf41-240">Come parte di hello attività di copia hello set di dati di input e output sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="ccf41-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="ccf41-241">Esempio: Copiare i dati da Blob di Azure tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ccf41-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="ccf41-242">viene illustrato l'esempio Hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ccf41-242">hello sample below shows:</span></span>

1. <span data-ttu-id="ccf41-243">Un servizio collegato di tipo [DocumentDB](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="ccf41-244">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ccf41-245">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ccf41-246">Un [set di dati](data-factory-create-datasets.md) di output di tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="ccf41-247">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="ccf41-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="ccf41-248">esempio Hello copia dati da blob di Azure tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ccf41-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="ccf41-249">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="ccf41-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ccf41-250">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ccf41-251">**Servizio collegato di Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="ccf41-252">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="ccf41-253">**Set di dati di output di Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="ccf41-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="ccf41-254">esempio Hello copia raccolta tooa dati denominato "Person".</span><span class="sxs-lookup"><span data-stu-id="ccf41-254">hello sample copies data tooa collection named “Person”.</span></span>

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
<span data-ttu-id="ccf41-255">esempio Hello pipeline copia i dati da Blob di Azure toohello raccolta persona in hello DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ccf41-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="ccf41-256">Come parte di hello attività di copia hello set di dati di input e output sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="ccf41-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="ccf41-257">Se utilizzato come input blob di esempio hello</span><span class="sxs-lookup"><span data-stu-id="ccf41-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="ccf41-258">Quindi l'output di hello JSON in DB Cosmos sarà come:</span><span class="sxs-lookup"><span data-stu-id="ccf41-258">Then hello output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="ccf41-259">Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate.</span><span class="sxs-lookup"><span data-stu-id="ccf41-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="ccf41-260">Data Factory di Azure consente gerarchia toodenote utente tramite **nestingSeparator**, ovvero "."</span><span class="sxs-lookup"><span data-stu-id="ccf41-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="ccf41-261">in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="ccf41-261">in this example.</span></span> <span data-ttu-id="ccf41-262">Con il separatore di hello, attività di copia hello genererà l'oggetto "Name" hello con elementi tre figli prima, intermedio e ultimo, in base too"Name.First", "Name.Middle" e "." in hello "Cognome" definizione di tabella.</span><span class="sxs-lookup"><span data-stu-id="ccf41-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="ccf41-263">Appendice</span><span class="sxs-lookup"><span data-stu-id="ccf41-263">Appendix</span></span>
1. <span data-ttu-id="ccf41-264">**Domanda:** hello aggiornamento di attività di copia del supporto dei record esistenti?</span><span class="sxs-lookup"><span data-stu-id="ccf41-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="ccf41-265">**Risposta:** No.</span><span class="sxs-lookup"><span data-stu-id="ccf41-265">**Answer:** No.</span></span>
2. <span data-ttu-id="ccf41-266">**Domanda:** funzionamento un nuovo tentativo di una copia tooAzure Cosmos DB gestiscono già copiati i record?</span><span class="sxs-lookup"><span data-stu-id="ccf41-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="ccf41-267">**Risposta:** se record hanno un campo "ID" e l'operazione di copia hello tenta tooinsert un record con hello stesso ID, l'operazione di copia hello genera un errore.</span><span class="sxs-lookup"><span data-stu-id="ccf41-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="ccf41-268">**Domanda:** Data Factory supporta il [partizionamento dei dati basato su hash o su intervalli](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="ccf41-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="ccf41-269">**Risposta:** No.</span><span class="sxs-lookup"><span data-stu-id="ccf41-269">**Answer:** No.</span></span>
4. <span data-ttu-id="ccf41-270">**Domanda:** è possibile specificare più raccolte di Azure Cosmos DB per una tabella?</span><span class="sxs-lookup"><span data-stu-id="ccf41-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="ccf41-271">**Risposta:** No.</span><span class="sxs-lookup"><span data-stu-id="ccf41-271">**Answer:** No.</span></span> <span data-ttu-id="ccf41-272">In questo momento, è possibile specificare solo una raccolta.</span><span class="sxs-lookup"><span data-stu-id="ccf41-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ccf41-273">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="ccf41-273">Performance and Tuning</span></span>
<span data-ttu-id="ccf41-274">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="ccf41-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
