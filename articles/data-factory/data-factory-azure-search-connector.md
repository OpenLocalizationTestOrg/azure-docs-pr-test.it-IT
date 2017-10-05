---
title: Push dei dati nell'indice di Ricerca con Azure Data Factory | Documentazione Microsoft
description: Informazioni su come eseguire il push dei dati nell'indice di Ricerca di Azure con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="a3d8e-103">Push dei dati in un indice di Ricerca di Azure con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a3d8e-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="a3d8e-104">Questo articolo descrive come usare l'attività di copia per eseguire il push dei dati da un archivio dati di origine supportato nell'indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="a3d8e-105">Gli archivi dati di origine supportati sono elencati nella colonna Origine della tabella [Origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a3d8e-106">Questo articolo si basa sull'articolo [Spostamento di dati e attività di copia](data-factory-data-movement-activities.md) , che offre una panoramica generale dello spostamento dei dati con attività di copia e delle combinazioni di archivi dati supportati.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="a3d8e-107">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="a3d8e-107">Enabling connectivity</span></span>
<span data-ttu-id="a3d8e-108">Per consentire la connessione del servizio Data Factory a un archivio dati locale, installare Gateway di gestione dati nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="a3d8e-109">È possibile installare il gateway nello stesso computer che ospita l'archivio dati di origine oppure in un computer diverso per evitare che si verifichi un conflitto con l'archivio dati per le risorse.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="a3d8e-110">Gateway di gestione dati consente di connettere le origini dati locali ai servizi cloud in modo sicuro e gestito.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="a3d8e-111">Vedere l’articolo [Spostare dati tra cloud e locale](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sui Gateway di Gestione dati.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a3d8e-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="a3d8e-112">Getting started</span></span>
<span data-ttu-id="a3d8e-113">È possibile creare una pipeline con un'attività di copia che esegue il push dei dati da un archivio dati di origine all'indice di Ricerca di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="a3d8e-114">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a3d8e-115">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a3d8e-116">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a3d8e-117">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a3d8e-118">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="a3d8e-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a3d8e-119">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a3d8e-120">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a3d8e-121">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a3d8e-122">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a3d8e-123">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a3d8e-124">Per un esempio con definizioni JSON per entità di data factory utilizzate per copiare dati nell'indice di Ricerca di Azure, vedere la sezione [Esempio JSON: Copiare dati da un'istanza di SQL Server locale all'indice di Ricerca di Azure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="a3d8e-125">Le sezioni seguenti riportano le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche dell'indice di Ricerca di Azure:</span><span class="sxs-lookup"><span data-stu-id="a3d8e-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a3d8e-126">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="a3d8e-126">Linked service properties</span></span>

<span data-ttu-id="a3d8e-127">La tabella seguente include le descrizioni degli elementi JSON specifici del servizio collegato Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="a3d8e-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a3d8e-128">Property</span></span> | <span data-ttu-id="a3d8e-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3d8e-129">Description</span></span> | <span data-ttu-id="a3d8e-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a3d8e-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="a3d8e-131">type</span><span class="sxs-lookup"><span data-stu-id="a3d8e-131">type</span></span> | <span data-ttu-id="a3d8e-132">La proprietà type deve essere impostata su **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="a3d8e-133">Sì</span><span class="sxs-lookup"><span data-stu-id="a3d8e-133">Yes</span></span> |
| <span data-ttu-id="a3d8e-134">URL</span><span class="sxs-lookup"><span data-stu-id="a3d8e-134">url</span></span> | <span data-ttu-id="a3d8e-135">URL del servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="a3d8e-136">sì</span><span class="sxs-lookup"><span data-stu-id="a3d8e-136">Yes</span></span> |
| <span data-ttu-id="a3d8e-137">key</span><span class="sxs-lookup"><span data-stu-id="a3d8e-137">key</span></span> | <span data-ttu-id="a3d8e-138">Chiave amministratore del servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="a3d8e-139">Sì</span><span class="sxs-lookup"><span data-stu-id="a3d8e-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="a3d8e-140">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="a3d8e-140">Dataset properties</span></span>

<span data-ttu-id="a3d8e-141">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo [Set di dati in Azure Data Factory](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="a3d8e-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a3d8e-142">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="a3d8e-143">La sezione **typeProperties** è diversa per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="a3d8e-144">Le proprietà della sezione typeProperties per un set di dati di tipo **AzureSearchIndex** sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3d8e-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="a3d8e-145">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a3d8e-145">Property</span></span> | <span data-ttu-id="a3d8e-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3d8e-146">Description</span></span> | <span data-ttu-id="a3d8e-147">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a3d8e-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="a3d8e-148">type</span><span class="sxs-lookup"><span data-stu-id="a3d8e-148">type</span></span> | <span data-ttu-id="a3d8e-149">La proprietà type deve essere impostata su **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="a3d8e-150">Sì</span><span class="sxs-lookup"><span data-stu-id="a3d8e-150">Yes</span></span> |
| <span data-ttu-id="a3d8e-151">indexName</span><span class="sxs-lookup"><span data-stu-id="a3d8e-151">indexName</span></span> | <span data-ttu-id="a3d8e-152">Nome dell'indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-152">Name of the Azure Search index.</span></span> <span data-ttu-id="a3d8e-153">Il servizio Data Factory non crea l'indice.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-153">Data Factory does not create the index.</span></span> <span data-ttu-id="a3d8e-154">L'indice deve essere presente in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="a3d8e-155">Sì</span><span class="sxs-lookup"><span data-stu-id="a3d8e-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="a3d8e-156">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="a3d8e-156">Copy activity properties</span></span>
<span data-ttu-id="a3d8e-157">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo relativo alla [creazione di pipeline](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="a3d8e-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a3d8e-158">Proprietà come nome, descrizione, tabelle di input e output e criteri diversi sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="a3d8e-159">Le proprietà disponibili nella sezione typeProperties variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="a3d8e-160">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a3d8e-161">Per l'attività di copia, quando il sink è del tipo **AzureSearchIndexSink**, nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3d8e-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a3d8e-162">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a3d8e-162">Property</span></span> | <span data-ttu-id="a3d8e-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3d8e-163">Description</span></span> | <span data-ttu-id="a3d8e-164">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="a3d8e-164">Allowed values</span></span> | <span data-ttu-id="a3d8e-165">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a3d8e-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="a3d8e-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="a3d8e-166">WriteBehavior</span></span> | <span data-ttu-id="a3d8e-167">Specifica se eseguire un'unione o una sostituzione quando nell'indice esiste già un documento.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="a3d8e-168">Vedere la [proprietà WriteBehavior](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="a3d8e-169">Merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="a3d8e-169">Merge (default)</span></span><br/><span data-ttu-id="a3d8e-170">Carica</span><span class="sxs-lookup"><span data-stu-id="a3d8e-170">Upload</span></span>| <span data-ttu-id="a3d8e-171">No</span><span class="sxs-lookup"><span data-stu-id="a3d8e-171">No</span></span> |
| <span data-ttu-id="a3d8e-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="a3d8e-172">WriteBatchSize</span></span> | <span data-ttu-id="a3d8e-173">Consente di caricare dati nell'indice di Ricerca di Azure quando le dimensioni del buffer raggiungono il valore indicato da writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="a3d8e-174">Per informazioni dettagliate, vedere la [proprietà WriteBatchSize](#writebatchsize-property).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="a3d8e-175">Da 1 a 1000.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-175">1 to 1,000.</span></span> <span data-ttu-id="a3d8e-176">Il valore predefinito è 1000.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-176">Default value is 1000.</span></span> | <span data-ttu-id="a3d8e-177">No</span><span class="sxs-lookup"><span data-stu-id="a3d8e-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="a3d8e-178">Proprietà WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="a3d8e-178">WriteBehavior property</span></span>
<span data-ttu-id="a3d8e-179">Durante la scrittura di dati, AzureSearchSink esegue operazioni di upsert.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="a3d8e-180">In altre parole, quando si scrive un documento il servizio Ricerca di Azure aggiorna il documento esistente anziché generare un'eccezione di conflitto se la chiave relativa esiste già nell'indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="a3d8e-181">Le operazioni di upsert eseguite da AzureSearchSink sono le seguenti (con AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="a3d8e-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="a3d8e-182">**Merge**: le colonne del nuovo documento vengono unite con quelle del documento esistente.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="a3d8e-183">Per le colonne del nuovo documento con valore Null, viene mantenuto il valore del documento esistente.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="a3d8e-184">**Upload**: il nuovo documento sostituisce quello esistente.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="a3d8e-185">Per le colonne del nuovo documento non specificate, il valore è impostato su Null indipendentemente dalla presenza o meno di un valore diverso da Null nel documento esistente.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="a3d8e-186">L'operazione predefinita è **Merge**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="a3d8e-187">Proprietà WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="a3d8e-187">WriteBatchSize Property</span></span>
<span data-ttu-id="a3d8e-188">Il servizio Ricerca di Azure supporta la scrittura di documenti come batch.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="a3d8e-189">Un batch può contenere da 1 a 1000 azioni</span><span class="sxs-lookup"><span data-stu-id="a3d8e-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="a3d8e-190">e un'azione gestisce un documento per eseguire l'operazione di caricamento/unione.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="a3d8e-191">Supporto dei tipi di dati</span><span class="sxs-lookup"><span data-stu-id="a3d8e-191">Data type support</span></span>
<span data-ttu-id="a3d8e-192">La tabella seguente indica se un tipo di dati di Ricerca di Azure è supportato o meno.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="a3d8e-193">Tipo di dati di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a3d8e-193">Azure Search data type</span></span> | <span data-ttu-id="a3d8e-194">Supportato nel sink di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a3d8e-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="a3d8e-195">String</span><span class="sxs-lookup"><span data-stu-id="a3d8e-195">String</span></span> | <span data-ttu-id="a3d8e-196">S</span><span class="sxs-lookup"><span data-stu-id="a3d8e-196">Y</span></span> |
| <span data-ttu-id="a3d8e-197">Int32</span><span class="sxs-lookup"><span data-stu-id="a3d8e-197">Int32</span></span> | <span data-ttu-id="a3d8e-198">S</span><span class="sxs-lookup"><span data-stu-id="a3d8e-198">Y</span></span> |
| <span data-ttu-id="a3d8e-199">Int64</span><span class="sxs-lookup"><span data-stu-id="a3d8e-199">Int64</span></span> | <span data-ttu-id="a3d8e-200">S</span><span class="sxs-lookup"><span data-stu-id="a3d8e-200">Y</span></span> |
| <span data-ttu-id="a3d8e-201">Double</span><span class="sxs-lookup"><span data-stu-id="a3d8e-201">Double</span></span> | <span data-ttu-id="a3d8e-202">S</span><span class="sxs-lookup"><span data-stu-id="a3d8e-202">Y</span></span> |
| <span data-ttu-id="a3d8e-203">Boolean</span><span class="sxs-lookup"><span data-stu-id="a3d8e-203">Boolean</span></span> | <span data-ttu-id="a3d8e-204">S</span><span class="sxs-lookup"><span data-stu-id="a3d8e-204">Y</span></span> |
| <span data-ttu-id="a3d8e-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a3d8e-205">DataTimeOffset</span></span> | <span data-ttu-id="a3d8e-206">S</span><span class="sxs-lookup"><span data-stu-id="a3d8e-206">Y</span></span> |
| <span data-ttu-id="a3d8e-207">String Array</span><span class="sxs-lookup"><span data-stu-id="a3d8e-207">String Array</span></span> | <span data-ttu-id="a3d8e-208">N</span><span class="sxs-lookup"><span data-stu-id="a3d8e-208">N</span></span> |
| <span data-ttu-id="a3d8e-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="a3d8e-209">GeographyPoint</span></span> | <span data-ttu-id="a3d8e-210">N</span><span class="sxs-lookup"><span data-stu-id="a3d8e-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="a3d8e-211">Esempio JSON: Copiare dati da un'istanza di SQL Server locale all'indice di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a3d8e-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="a3d8e-212">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="a3d8e-212">The following sample shows:</span></span>

1.  <span data-ttu-id="a3d8e-213">Un servizio collegato di tipo [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="a3d8e-214">Un servizio collegato di tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="a3d8e-215">Un [set di dati](data-factory-create-datasets.md) di tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="a3d8e-216">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="a3d8e-217">Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="a3d8e-218">Nell'esempio i dati della serie temporale vengono copiati ogni ora da un database di SQL Server locale in un indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="a3d8e-219">Le proprietà JSON usate in questo esempio sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="a3d8e-220">Come primo passaggio è necessario configurare Gateway di gestione dati nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="a3d8e-221">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="a3d8e-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a3d8e-222">**Servizio collegato Ricerca di Azure**</span><span class="sxs-lookup"><span data-stu-id="a3d8e-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="a3d8e-223">**Servizio collegato di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="a3d8e-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="a3d8e-224">**Set di dati input di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="a3d8e-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="a3d8e-225">L'esempio presuppone che sia stata creata una tabella "MyTable" in SQL Server e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="a3d8e-226">È possibile eseguire query su più tabelle all'interno dello stesso database usando un singolo set di dati, ma come typeProperty tableName del set di dati deve essere usata una sola tabella.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="a3d8e-227">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno a Data Factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="a3d8e-228">**Set di dati di output di Ricerca di Azure**</span><span class="sxs-lookup"><span data-stu-id="a3d8e-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="a3d8e-229">Nell'esempio i dati vengono copiati in un indice di Ricerca di Azure denominato **products**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="a3d8e-230">Il servizio Data Factory non crea l'indice.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-230">Data Factory does not create the index.</span></span> <span data-ttu-id="a3d8e-231">Per eseguire il test dell'esempio, creare un indice con questo nome.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="a3d8e-232">Creare l'indice di Ricerca di Azure con lo stesso numero di colonne presente nel set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="a3d8e-233">Le nuove voci vengono aggiunte all'indice di Ricerca di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-233">New entries are added to the Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="a3d8e-234">**Attività di copia in una pipeline con un'origine SQL e il sink dell'indice di Ricerca di Azure:**</span><span class="sxs-lookup"><span data-stu-id="a3d8e-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="a3d8e-235">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a3d8e-236">Nella definizione JSON della pipeline il tipo **source** è impostato su **SqlSource** e il tipo **sink** è impostato su **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="a3d8e-237">La query SQL specificata per la proprietà **SqlReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="a3d8e-238">Se si copiano dati da un archivio dati cloud a Ricerca di Azure, la proprietà `executionLocation` è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="a3d8e-239">Il frammento JSON seguente mostra la modifica necessaria nell'attività di copia `typeProperties` come esempio.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="a3d8e-240">Per informazioni sui valori supportati e altri dettagli, vedere la sezione [Copiare dati tra archivi dati cloud](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="a3d8e-241">Copiare da un'origine cloud</span><span class="sxs-lookup"><span data-stu-id="a3d8e-241">Copy from a cloud source</span></span>
<span data-ttu-id="a3d8e-242">Se si copiano dati da un archivio dati cloud a Ricerca di Azure, la proprietà `executionLocation` è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="a3d8e-243">Il frammento JSON seguente mostra la modifica necessaria nell'attività di copia `typeProperties` come esempio.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="a3d8e-244">Per informazioni sui valori supportati e altri dettagli, vedere la sezione [Copiare dati tra archivi dati cloud](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="a3d8e-245">È anche possibile eseguire il mapping delle colonne del set di dati di origine alle colonne del set di dati sink nella definizione dell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="a3d8e-246">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a3d8e-247">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="a3d8e-247">Performance and tuning</span></span>  
<span data-ttu-id="a3d8e-248">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati (attività di copia) e sui vari modi per ottimizzarle, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a3d8e-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d8e-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3d8e-249">Next steps</span></span>
<span data-ttu-id="a3d8e-250">Vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3d8e-250">See the following articles:</span></span>

* <span data-ttu-id="a3d8e-251">[Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a3d8e-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
