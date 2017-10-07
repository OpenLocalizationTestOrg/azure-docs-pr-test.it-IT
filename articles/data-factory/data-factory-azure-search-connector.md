---
title: indice di tooSearch aaaPush dati utilizzando Data Factory | Documenti Microsoft
description: Per ulteriori informazioni vedere toopush dati tooAzure indice di ricerca usando Azure Data Factory.
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
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="ab2b6-103">Push di dati tooan indice di ricerca Azure mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ab2b6-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="ab2b6-104">In questo articolo viene descritto come dati toopush di attività di copia toouse hello dai dati di origine supportata archiviano tooAzure indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="ab2b6-105">Archivi dati di origine supportati sono elencati nella colonna di origine hello di hello [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ab2b6-106">In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia e combinazioni di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="ab2b6-107">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="ab2b6-107">Enabling connectivity</span></span>
<span data-ttu-id="ab2b6-108">servizio Data Factory tooallow connettersi tooan archivio di dati locale, si installa il Gateway di gestione di dati nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="ab2b6-109">È possibile installare gateway in hello nello stesso computer che ospita i dati di origine hello archiviare o in tooavoid un computer separato competono per le risorse con i dati di hello archivio.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="ab2b6-110">Gateway di gestione dati si connette servizi toocloud origini di dati locali in modo sicuro e gestito.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="ab2b6-111">Vedere l’articolo [Spostare dati tra cloud e locale](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sui Gateway di Gestione dati.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ab2b6-112">introduttiva</span><span class="sxs-lookup"><span data-stu-id="ab2b6-112">Getting started</span></span>
<span data-ttu-id="ab2b6-113">È possibile creare una pipeline con un'attività di copia che inserisce i dati da un indice di ricerca di origine dati archivio tooAzure tramite diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="ab2b6-114">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ab2b6-115">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ab2b6-116">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ab2b6-117">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ab2b6-118">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ab2b6-119">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ab2b6-120">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ab2b6-121">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ab2b6-122">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ab2b6-123">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ab2b6-124">Per un esempio con le definizioni di JSON per le entità Data Factory indice di ricerca tooAzure toocopy utilizzati dati, vedere [esempio JSON: copiare i dati dall'indice di ricerca tooAzure SQL Server on-premise](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="ab2b6-125">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure indice di ricerca:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ab2b6-126">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="ab2b6-126">Linked service properties</span></span>

<span data-ttu-id="ab2b6-127">Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON che il servizio di ricerca di Azure collegati toohello specifico.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="ab2b6-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ab2b6-128">Property</span></span> | <span data-ttu-id="ab2b6-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab2b6-129">Description</span></span> | <span data-ttu-id="ab2b6-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ab2b6-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ab2b6-131">type</span><span class="sxs-lookup"><span data-stu-id="ab2b6-131">type</span></span> | <span data-ttu-id="ab2b6-132">proprietà di tipo Hello deve essere impostata su: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="ab2b6-133">Sì</span><span class="sxs-lookup"><span data-stu-id="ab2b6-133">Yes</span></span> |
| <span data-ttu-id="ab2b6-134">URL</span><span class="sxs-lookup"><span data-stu-id="ab2b6-134">url</span></span> | <span data-ttu-id="ab2b6-135">URL per il servizio di ricerca di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="ab2b6-136">Sì</span><span class="sxs-lookup"><span data-stu-id="ab2b6-136">Yes</span></span> |
| <span data-ttu-id="ab2b6-137">key</span><span class="sxs-lookup"><span data-stu-id="ab2b6-137">key</span></span> | <span data-ttu-id="ab2b6-138">Chiave di amministrazione per hello del servizio di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="ab2b6-139">Sì</span><span class="sxs-lookup"><span data-stu-id="ab2b6-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="ab2b6-140">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="ab2b6-140">Dataset properties</span></span>

<span data-ttu-id="ab2b6-141">Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ab2b6-142">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="ab2b6-143">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="ab2b6-144">sezione Hello typeProperties per un set di dati di tipo hello **AzureSearchIndex** è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="ab2b6-145">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ab2b6-145">Property</span></span> | <span data-ttu-id="ab2b6-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab2b6-146">Description</span></span> | <span data-ttu-id="ab2b6-147">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ab2b6-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ab2b6-148">type</span><span class="sxs-lookup"><span data-stu-id="ab2b6-148">type</span></span> | <span data-ttu-id="ab2b6-149">proprietà di tipo Hello deve essere impostata troppo**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="ab2b6-150">Sì</span><span class="sxs-lookup"><span data-stu-id="ab2b6-150">Yes</span></span> |
| <span data-ttu-id="ab2b6-151">indexName</span><span class="sxs-lookup"><span data-stu-id="ab2b6-151">indexName</span></span> | <span data-ttu-id="ab2b6-152">Nome dell'indice di ricerca di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="ab2b6-153">Data Factory di creare l'indice di hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="ab2b6-154">indice di Hello deve esistere in ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="ab2b6-155">Sì</span><span class="sxs-lookup"><span data-stu-id="ab2b6-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="ab2b6-156">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="ab2b6-156">Copy activity properties</span></span>
<span data-ttu-id="ab2b6-157">Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di attività, vedere hello [creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ab2b6-158">Proprietà come nome, descrizione, tabelle di input e output e criteri diversi sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="ab2b6-159">Mentre le proprietà disponibili nella sezione typeProperties hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="ab2b6-160">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ab2b6-161">Per attività di copia, quando il sink di hello è di tipo hello **AzureSearchIndexSink**, hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="ab2b6-162">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ab2b6-162">Property</span></span> | <span data-ttu-id="ab2b6-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab2b6-163">Description</span></span> | <span data-ttu-id="ab2b6-164">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="ab2b6-164">Allowed values</span></span> | <span data-ttu-id="ab2b6-165">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ab2b6-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="ab2b6-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="ab2b6-166">WriteBehavior</span></span> | <span data-ttu-id="ab2b6-167">Specifica se toomerge o Sostituisci quando un documento già presente nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="ab2b6-168">Vedere hello [WriteBehavior proprietà](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="ab2b6-169">Merge (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="ab2b6-169">Merge (default)</span></span><br/><span data-ttu-id="ab2b6-170">Carica</span><span class="sxs-lookup"><span data-stu-id="ab2b6-170">Upload</span></span>| <span data-ttu-id="ab2b6-171">No</span><span class="sxs-lookup"><span data-stu-id="ab2b6-171">No</span></span> |
| <span data-ttu-id="ab2b6-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="ab2b6-172">WriteBatchSize</span></span> | <span data-ttu-id="ab2b6-173">Carica i dati nell'indice di ricerca di Azure hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="ab2b6-174">Vedere hello [viene raggiunto WriteBatchSize proprietà](#writebatchsize-property) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="ab2b6-175">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-175">1 too1,000.</span></span> <span data-ttu-id="ab2b6-176">Il valore predefinito è 1000.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-176">Default value is 1000.</span></span> | <span data-ttu-id="ab2b6-177">No</span><span class="sxs-lookup"><span data-stu-id="ab2b6-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="ab2b6-178">Proprietà WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="ab2b6-178">WriteBehavior property</span></span>
<span data-ttu-id="ab2b6-179">Durante la scrittura di dati, AzureSearchSink esegue operazioni di upsert.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="ab2b6-180">In altre parole, quando si scrive un documento, se la chiave di documento hello esiste già nell'indice di ricerca di Azure hello, ricerca di Azure Aggiorna documento esistente hello anziché generare un'eccezione di conflitto.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="ab2b6-181">Hello AzureSearchSink fornisce hello seguenti due comportamenti upsert (utilizzando il SDK AzureSearch):</span><span class="sxs-lookup"><span data-stu-id="ab2b6-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="ab2b6-182">**Merge**: combinare tutte le colonne di hello nel documento nuovo hello con hello uno esistente.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="ab2b6-183">Per le colonne con valore null nel nuovo documento hello, viene mantenuto il valore di hello in hello uno esistente.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="ab2b6-184">**Caricare**: sostituisce documento nuovo hello hello uno esistente.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="ab2b6-185">Per le colonne non è specificate nel documento nuovo hello, hello è impostato toonull se è presente un valore non null nel documento di hello esistente o non.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="ab2b6-186">comportamento predefinito di Hello **Merge**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="ab2b6-187">Proprietà WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="ab2b6-187">WriteBatchSize Property</span></span>
<span data-ttu-id="ab2b6-188">Il servizio Ricerca di Azure supporta la scrittura di documenti come batch.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="ab2b6-189">Un batch può contenere 1 too1, azioni 000.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="ab2b6-190">Un'azione gestisce un'operazione di caricamento/merge hello di tooperform documento.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="ab2b6-191">Supporto dei tipi di dati</span><span class="sxs-lookup"><span data-stu-id="ab2b6-191">Data type support</span></span>
<span data-ttu-id="ab2b6-192">Hello nella tabella seguente specifica se un tipo di dati di ricerca di Azure è supportato o meno.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="ab2b6-193">Tipo di dati di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="ab2b6-193">Azure Search data type</span></span> | <span data-ttu-id="ab2b6-194">Supportato nel sink di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="ab2b6-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="ab2b6-195">String</span><span class="sxs-lookup"><span data-stu-id="ab2b6-195">String</span></span> | <span data-ttu-id="ab2b6-196">S</span><span class="sxs-lookup"><span data-stu-id="ab2b6-196">Y</span></span> |
| <span data-ttu-id="ab2b6-197">Int32</span><span class="sxs-lookup"><span data-stu-id="ab2b6-197">Int32</span></span> | <span data-ttu-id="ab2b6-198">S</span><span class="sxs-lookup"><span data-stu-id="ab2b6-198">Y</span></span> |
| <span data-ttu-id="ab2b6-199">Int64</span><span class="sxs-lookup"><span data-stu-id="ab2b6-199">Int64</span></span> | <span data-ttu-id="ab2b6-200">S</span><span class="sxs-lookup"><span data-stu-id="ab2b6-200">Y</span></span> |
| <span data-ttu-id="ab2b6-201">Double</span><span class="sxs-lookup"><span data-stu-id="ab2b6-201">Double</span></span> | <span data-ttu-id="ab2b6-202">S</span><span class="sxs-lookup"><span data-stu-id="ab2b6-202">Y</span></span> |
| <span data-ttu-id="ab2b6-203">Boolean</span><span class="sxs-lookup"><span data-stu-id="ab2b6-203">Boolean</span></span> | <span data-ttu-id="ab2b6-204">S</span><span class="sxs-lookup"><span data-stu-id="ab2b6-204">Y</span></span> |
| <span data-ttu-id="ab2b6-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ab2b6-205">DataTimeOffset</span></span> | <span data-ttu-id="ab2b6-206">S</span><span class="sxs-lookup"><span data-stu-id="ab2b6-206">Y</span></span> |
| <span data-ttu-id="ab2b6-207">String Array</span><span class="sxs-lookup"><span data-stu-id="ab2b6-207">String Array</span></span> | <span data-ttu-id="ab2b6-208">N</span><span class="sxs-lookup"><span data-stu-id="ab2b6-208">N</span></span> |
| <span data-ttu-id="ab2b6-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="ab2b6-209">GeographyPoint</span></span> | <span data-ttu-id="ab2b6-210">N</span><span class="sxs-lookup"><span data-stu-id="ab2b6-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="ab2b6-211">Esempio JSON: copiare i dati dall'indice di ricerca tooAzure SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="ab2b6-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="ab2b6-212">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="ab2b6-213">Un servizio collegato di tipo [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="ab2b6-214">Un servizio collegato di tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="ab2b6-215">Un [set di dati](data-factory-create-datasets.md) di tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="ab2b6-216">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="ab2b6-217">Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ab2b6-218">esempio Hello copia i dati delle serie temporali da un indice di ricerca di Azure locale tooan database di SQL Server ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="ab2b6-219">proprietà JSON Hello utilizzate in questo esempio sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="ab2b6-220">Come primo passaggio, configurare il gateway di gestione dati hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="ab2b6-221">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="ab2b6-222">**Servizio collegato Ricerca di Azure**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="ab2b6-223">**Servizio collegato di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="ab2b6-224">**Set di dati input di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="ab2b6-225">esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Server e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="ab2b6-226">È possibile eseguire query su più tabelle all'interno di hello stesso database con un singolo set di dati, ma una singola tabella deve essere utilizzato per typeProperty tableName hello del dataset.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="ab2b6-227">L'impostazione "external": "true" informa il servizio Data Factory hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="ab2b6-228">**Set di dati di output di Ricerca di Azure**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="ab2b6-229">Hello esempio copie dei dati tooan Azure indice di ricerca denominato **prodotti**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="ab2b6-230">Data Factory di creare l'indice di hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="ab2b6-231">hello tootest di esempio, creare un indice con questo nome.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="ab2b6-232">Creare l'indice di ricerca di Azure hello con hello stesso numero di colonne come set di dati input hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="ab2b6-233">Vengono aggiunte nuove voci toohello indice di ricerca di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-233">New entries are added toohello Azure Search index every hour.</span></span>

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

<span data-ttu-id="ab2b6-234">**Attività di copia in una pipeline con un'origine SQL e il sink dell'indice di Ricerca di Azure:**</span><span class="sxs-lookup"><span data-stu-id="ab2b6-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="ab2b6-235">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ab2b6-236">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="ab2b6-237">query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

<span data-ttu-id="ab2b6-238">Se si copiano dati da un archivio dati cloud a Ricerca di Azure, la proprietà `executionLocation` è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="ab2b6-239">frammento di codice JSON seguente Hello Mostra hello modifica necessaria nell'attività di copia `typeProperties` come esempio.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="ab2b6-240">Per informazioni sui valori supportati e altri dettagli, vedere la sezione [Copiare dati tra archivi dati cloud](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="ab2b6-241">Copiare da un'origine cloud</span><span class="sxs-lookup"><span data-stu-id="ab2b6-241">Copy from a cloud source</span></span>
<span data-ttu-id="ab2b6-242">Se si copiano dati da un archivio dati cloud a Ricerca di Azure, la proprietà `executionLocation` è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="ab2b6-243">frammento di codice JSON seguente Hello Mostra hello modifica necessaria nell'attività di copia `typeProperties` come esempio.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="ab2b6-244">Per informazioni sui valori supportati e altri dettagli, vedere la sezione [Copiare dati tra archivi dati cloud](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="ab2b6-245">È anche possibile mappare le colonne di origine toocolumns di set di dati dal set di dati di sink nella definizione di attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="ab2b6-246">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b6-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ab2b6-247">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="ab2b6-247">Performance and tuning</span></span>  
<span data-ttu-id="ab2b6-248">Vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab2b6-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab2b6-249">Next steps</span></span>
<span data-ttu-id="ab2b6-250">Vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="ab2b6-250">See hello following articles:</span></span>

* <span data-ttu-id="ab2b6-251">[Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="ab2b6-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
