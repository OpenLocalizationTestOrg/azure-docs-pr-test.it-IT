---
title: dati aaaMove da Amazon Redshift utilizzando Data Factory | Documenti Microsoft
description: Informazioni su come dati toomove da Amazon Redshift usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="76747-103">Spostare i dati da Amazon Redshift usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="76747-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="76747-104">Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove da Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="76747-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="76747-105">articolo Hello si basa sulle hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="76747-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="76747-106">È possibile copiare i dati dall'archivio dati di Amazon Redshift tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="76747-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="76747-107">Per un elenco di archivi dati come sink è supportato dall'attività di copia hello, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="76747-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="76747-108">Data factory di supporta attualmente lo spostamento dei dati dagli archivi dati di Amazon Redshift tooother, ma non per lo spostamento dei dati da altri tooAmazon di archivi dati Redshift.</span><span class="sxs-lookup"><span data-stu-id="76747-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76747-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="76747-109">Prerequisites</span></span>
* <span data-ttu-id="76747-110">Se si stanno spostando i dati di archivio tooan locale, installare [Gateway di gestione dati](data-factory-data-management-gateway.md) in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="76747-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="76747-111">Quindi, Gateway di gestione dati Grant (utilizzare l'indirizzo IP del computer hello) hello tooAmazon Redshift cluster di accesso.</span><span class="sxs-lookup"><span data-stu-id="76747-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="76747-112">Vedere [cluster toohello di accesso autorizza](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="76747-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="76747-113">Se si stanno spostando l'archivio dati di Azure tooan di dati, vedere [gli intervalli IP di Azure Data Center](https://www.microsoft.com/download/details.aspx?id=41653) per indirizzo IP di calcolo hello e gli intervalli SQL utilizzati da hello data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="76747-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="76747-114">introduttiva</span><span class="sxs-lookup"><span data-stu-id="76747-114">Getting started</span></span>
<span data-ttu-id="76747-115">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine Amazon Redshift usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="76747-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="76747-116">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="76747-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="76747-117">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="76747-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="76747-118">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="76747-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="76747-119">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="76747-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="76747-120">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="76747-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="76747-121">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="76747-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="76747-122">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="76747-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="76747-123">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="76747-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="76747-124">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="76747-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="76747-125">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76747-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="76747-126">Per un esempio con le definizioni per le entità Data Factory dati toocopy utilizzato da un archivio dati Amazon Redshift JSON, vedere [esempio JSON: copiare i dati da Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="76747-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="76747-127">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAmazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="76747-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="76747-128">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="76747-128">Linked service properties</span></span>
<span data-ttu-id="76747-129">Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooAmazon servizio Redshift collegato.</span><span class="sxs-lookup"><span data-stu-id="76747-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="76747-130">Proprietà</span><span class="sxs-lookup"><span data-stu-id="76747-130">Property</span></span> | <span data-ttu-id="76747-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76747-131">Description</span></span> | <span data-ttu-id="76747-132">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="76747-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76747-133">type</span><span class="sxs-lookup"><span data-stu-id="76747-133">type</span></span> |<span data-ttu-id="76747-134">proprietà di tipo Hello deve essere impostata su: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="76747-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="76747-135">Sì</span><span class="sxs-lookup"><span data-stu-id="76747-135">Yes</span></span> |
| <span data-ttu-id="76747-136">server</span><span class="sxs-lookup"><span data-stu-id="76747-136">server</span></span> |<span data-ttu-id="76747-137">IP il nome host o indirizzo del server di Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="76747-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="76747-138">Sì</span><span class="sxs-lookup"><span data-stu-id="76747-138">Yes</span></span> |
| <span data-ttu-id="76747-139">port</span><span class="sxs-lookup"><span data-stu-id="76747-139">port</span></span> |<span data-ttu-id="76747-140">numero di Hello di porta TCP hello hello server Amazon Redshift utilizza toolisten per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="76747-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="76747-141">No, valore predefinito: 5439</span><span class="sxs-lookup"><span data-stu-id="76747-141">No, default value: 5439</span></span> |
| <span data-ttu-id="76747-142">database</span><span class="sxs-lookup"><span data-stu-id="76747-142">database</span></span> |<span data-ttu-id="76747-143">Nome del database Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="76747-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="76747-144">Sì</span><span class="sxs-lookup"><span data-stu-id="76747-144">Yes</span></span> |
| <span data-ttu-id="76747-145">username</span><span class="sxs-lookup"><span data-stu-id="76747-145">username</span></span> |<span data-ttu-id="76747-146">Nome dell'utente che dispone di accesso toohello database.</span><span class="sxs-lookup"><span data-stu-id="76747-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="76747-147">Sì</span><span class="sxs-lookup"><span data-stu-id="76747-147">Yes</span></span> |
| <span data-ttu-id="76747-148">password</span><span class="sxs-lookup"><span data-stu-id="76747-148">password</span></span> |<span data-ttu-id="76747-149">Password dell'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="76747-149">Password for hello user account.</span></span> |<span data-ttu-id="76747-150">Sì</span><span class="sxs-lookup"><span data-stu-id="76747-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="76747-151">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="76747-151">Dataset properties</span></span>
<span data-ttu-id="76747-152">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="76747-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="76747-153">Le sezioni come struttura, disponibilità e criteri sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="76747-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="76747-154">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="76747-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="76747-155">Fornisce informazioni sul percorso hello hello dati nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="76747-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="76747-156">sezione Hello typeProperties per set di dati di tipo **RelationalTable** (che include set di dati di Amazon Redshift) ha le proprietà seguenti hello</span><span class="sxs-lookup"><span data-stu-id="76747-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="76747-157">Proprietà</span><span class="sxs-lookup"><span data-stu-id="76747-157">Property</span></span> | <span data-ttu-id="76747-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76747-158">Description</span></span> | <span data-ttu-id="76747-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="76747-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76747-160">tableName</span><span class="sxs-lookup"><span data-stu-id="76747-160">tableName</span></span> |<span data-ttu-id="76747-161">Nome della tabella hello hello Amazon Redshift in database in cui il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="76747-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="76747-162">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="76747-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="76747-163">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="76747-163">Copy activity properties</span></span>
<span data-ttu-id="76747-164">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="76747-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="76747-165">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="76747-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="76747-166">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="76747-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="76747-167">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="76747-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="76747-168">Quando l'origine dell'attività di copia è di tipo **RelationalSource** (che include Amazon Redshift), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="76747-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="76747-169">Proprietà</span><span class="sxs-lookup"><span data-stu-id="76747-169">Property</span></span> | <span data-ttu-id="76747-170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="76747-170">Description</span></span> | <span data-ttu-id="76747-171">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="76747-171">Allowed values</span></span> | <span data-ttu-id="76747-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="76747-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="76747-173">query</span><span class="sxs-lookup"><span data-stu-id="76747-173">query</span></span> |<span data-ttu-id="76747-174">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="76747-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="76747-175">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="76747-175">SQL query string.</span></span> <span data-ttu-id="76747-176">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="76747-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="76747-177">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="76747-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="76747-178">Esempio JSON: copiare i dati da Amazon Redshift tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="76747-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="76747-179">Questo esempio viene illustrato come toocopy dati da un Amazon Redshift database tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="76747-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="76747-180">Tuttavia, i dati possono essere copiati **direttamente** tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76747-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="76747-181">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="76747-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="76747-182">Un servizio collegato di tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="76747-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="76747-183">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="76747-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="76747-184">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="76747-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="76747-185">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="76747-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="76747-186">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="76747-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="76747-187">esempio Hello copia dati da un risultato della query nel blob tooa Amazon Redshift ogni ora.</span><span class="sxs-lookup"><span data-stu-id="76747-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="76747-188">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="76747-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="76747-189">**Servizio collegato Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="76747-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="76747-190">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="76747-190">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="76747-191">**Set di dati di input Redshift Amazon:**</span><span class="sxs-lookup"><span data-stu-id="76747-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="76747-192">Impostazione `"external": true` informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="76747-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="76747-193">Impostare tootrue questa proprietà su un set di dati di input che non è stato generato da un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="76747-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="76747-194">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="76747-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="76747-195">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="76747-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="76747-196">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="76747-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="76747-197">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="76747-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="76747-198">**Attività di copia in una pipeline con origine Amazon Redshift (RelationalSource) e sink BLOB.**</span><span class="sxs-lookup"><span data-stu-id="76747-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="76747-199">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="76747-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="76747-200">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="76747-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="76747-201">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="76747-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="76747-202">Tipo di mappatura di Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="76747-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="76747-203">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="76747-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="76747-204">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="76747-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="76747-205">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="76747-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="76747-206">Quando si spostano dati tooAmazon Redshift, hello seguendo i mapping viene utilizzato da Amazon Redshift tipi too.NET tipi.</span><span class="sxs-lookup"><span data-stu-id="76747-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="76747-207">Tipo di Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="76747-207">Amazon Redshift Type</span></span> | <span data-ttu-id="76747-208">Tipo basato su .Net</span><span class="sxs-lookup"><span data-stu-id="76747-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="76747-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="76747-209">SMALLINT</span></span> |<span data-ttu-id="76747-210">Int16</span><span class="sxs-lookup"><span data-stu-id="76747-210">Int16</span></span> |
| <span data-ttu-id="76747-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="76747-211">INTEGER</span></span> |<span data-ttu-id="76747-212">Int32</span><span class="sxs-lookup"><span data-stu-id="76747-212">Int32</span></span> |
| <span data-ttu-id="76747-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="76747-213">BIGINT</span></span> |<span data-ttu-id="76747-214">Int64</span><span class="sxs-lookup"><span data-stu-id="76747-214">Int64</span></span> |
| <span data-ttu-id="76747-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="76747-215">DECIMAL</span></span> |<span data-ttu-id="76747-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="76747-216">Decimal</span></span> |
| <span data-ttu-id="76747-217">REAL</span><span class="sxs-lookup"><span data-stu-id="76747-217">REAL</span></span> |<span data-ttu-id="76747-218">Single</span><span class="sxs-lookup"><span data-stu-id="76747-218">Single</span></span> |
| <span data-ttu-id="76747-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="76747-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="76747-220">Double</span><span class="sxs-lookup"><span data-stu-id="76747-220">Double</span></span> |
| <span data-ttu-id="76747-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="76747-221">BOOLEAN</span></span> |<span data-ttu-id="76747-222">String</span><span class="sxs-lookup"><span data-stu-id="76747-222">String</span></span> |
| <span data-ttu-id="76747-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="76747-223">CHAR</span></span> |<span data-ttu-id="76747-224">String</span><span class="sxs-lookup"><span data-stu-id="76747-224">String</span></span> |
| <span data-ttu-id="76747-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="76747-225">VARCHAR</span></span> |<span data-ttu-id="76747-226">String</span><span class="sxs-lookup"><span data-stu-id="76747-226">String</span></span> |
| <span data-ttu-id="76747-227">DATE</span><span class="sxs-lookup"><span data-stu-id="76747-227">DATE</span></span> |<span data-ttu-id="76747-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="76747-228">DateTime</span></span> |
| <span data-ttu-id="76747-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="76747-229">TIMESTAMP</span></span> |<span data-ttu-id="76747-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="76747-230">DateTime</span></span> |
| <span data-ttu-id="76747-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="76747-231">TEXT</span></span> |<span data-ttu-id="76747-232">String</span><span class="sxs-lookup"><span data-stu-id="76747-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="76747-233">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="76747-233">Map source toosink columns</span></span>
<span data-ttu-id="76747-234">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="76747-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="76747-235">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="76747-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="76747-236">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="76747-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="76747-237">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="76747-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="76747-238">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="76747-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="76747-239">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="76747-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="76747-240">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="76747-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="76747-241">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="76747-241">Performance and Tuning</span></span>
<span data-ttu-id="76747-242">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="76747-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76747-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76747-243">Next Steps</span></span>
<span data-ttu-id="76747-244">Vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="76747-244">See hello following articles:</span></span>

* <span data-ttu-id="76747-245">[Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="76747-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
