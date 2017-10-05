---
title: Spostare dati da una tabella Web usando Azure Data Factory | Documentazione Microsoft
description: Informazioni su come spostare dati da una tabella in una pagina Web con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="11cb9-103">Spostare i dati da un'origine tabella Web con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="11cb9-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="11cb9-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare dati da una tabella in una pagina Web in un archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="11cb9-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="11cb9-105">Questo articolo si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con attività di copia e l'elenco degli archivi dati supportati come origini/sink.</span><span class="sxs-lookup"><span data-stu-id="11cb9-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="11cb9-106">Data Factory supporta attualmente solo lo spostamento di dati da una tabella Web ad altri archivi dati, non da altri archivi dati a una tabella Web.</span><span class="sxs-lookup"><span data-stu-id="11cb9-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11cb9-107">Questo connettore Web attualmente supporta soltanto l'estrazione del contenuto della tabella da una pagina HTML.</span><span class="sxs-lookup"><span data-stu-id="11cb9-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="11cb9-108">Per recuperare dati da un endpoint HTTP/s, usare invece il [connettore HTTP](data-factory-http-connector.md).</span><span class="sxs-lookup"><span data-stu-id="11cb9-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="11cb9-109">Introduzione</span><span class="sxs-lookup"><span data-stu-id="11cb9-109">Getting started</span></span>
<span data-ttu-id="11cb9-110">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="11cb9-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="11cb9-111">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="11cb9-112">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="11cb9-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="11cb9-113">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="11cb9-114">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="11cb9-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="11cb9-115">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="11cb9-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="11cb9-116">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="11cb9-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="11cb9-117">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="11cb9-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="11cb9-118">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="11cb9-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="11cb9-119">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="11cb9-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="11cb9-120">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="11cb9-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="11cb9-121">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da una tabella Web, vedere la sezione [Esempio JSON: Copiare dati da una tabella Web a BLOB di Azure](#json-example-copy-data-from-web-table-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="11cb9-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="11cb9-122">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di una tabella Web:</span><span class="sxs-lookup"><span data-stu-id="11cb9-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="11cb9-123">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="11cb9-123">Linked service properties</span></span>
<span data-ttu-id="11cb9-124">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato Web.</span><span class="sxs-lookup"><span data-stu-id="11cb9-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="11cb9-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="11cb9-125">Property</span></span> | <span data-ttu-id="11cb9-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="11cb9-126">Description</span></span> | <span data-ttu-id="11cb9-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="11cb9-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11cb9-128">type</span><span class="sxs-lookup"><span data-stu-id="11cb9-128">type</span></span> |<span data-ttu-id="11cb9-129">La proprietà type deve essere impostata su: **Web**</span><span class="sxs-lookup"><span data-stu-id="11cb9-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="11cb9-130">Sì</span><span class="sxs-lookup"><span data-stu-id="11cb9-130">Yes</span></span> |
| <span data-ttu-id="11cb9-131">Url</span><span class="sxs-lookup"><span data-stu-id="11cb9-131">Url</span></span> |<span data-ttu-id="11cb9-132">URL dell'origine Web</span><span class="sxs-lookup"><span data-stu-id="11cb9-132">URL to the Web source</span></span> |<span data-ttu-id="11cb9-133">Sì</span><span class="sxs-lookup"><span data-stu-id="11cb9-133">Yes</span></span> |
| <span data-ttu-id="11cb9-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="11cb9-134">authenticationType</span></span> |<span data-ttu-id="11cb9-135">Anonimo.</span><span class="sxs-lookup"><span data-stu-id="11cb9-135">Anonymous.</span></span> |<span data-ttu-id="11cb9-136">Sì</span><span class="sxs-lookup"><span data-stu-id="11cb9-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="11cb9-137">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="11cb9-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="11cb9-138">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="11cb9-138">Dataset properties</span></span>
<span data-ttu-id="11cb9-139">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="11cb9-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="11cb9-140">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="11cb9-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="11cb9-141">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="11cb9-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="11cb9-142">La sezione typeProperties per il set di dati di tipo **WebTable** presenta le proprietà seguenti</span><span class="sxs-lookup"><span data-stu-id="11cb9-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="11cb9-143">Proprietà</span><span class="sxs-lookup"><span data-stu-id="11cb9-143">Property</span></span> | <span data-ttu-id="11cb9-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="11cb9-144">Description</span></span> | <span data-ttu-id="11cb9-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="11cb9-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="11cb9-146">type</span><span class="sxs-lookup"><span data-stu-id="11cb9-146">type</span></span> |<span data-ttu-id="11cb9-147">Tipo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="11cb9-147">type of the dataset.</span></span> <span data-ttu-id="11cb9-148">Deve essere impostato su **WebTable**</span><span class="sxs-lookup"><span data-stu-id="11cb9-148">must be set to **WebTable**</span></span> |<span data-ttu-id="11cb9-149">Sì</span><span class="sxs-lookup"><span data-stu-id="11cb9-149">Yes</span></span> |
| <span data-ttu-id="11cb9-150">path</span><span class="sxs-lookup"><span data-stu-id="11cb9-150">path</span></span> |<span data-ttu-id="11cb9-151">URL relativo della risorsa che contiene la tabella.</span><span class="sxs-lookup"><span data-stu-id="11cb9-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="11cb9-152">No.</span><span class="sxs-lookup"><span data-stu-id="11cb9-152">No.</span></span> <span data-ttu-id="11cb9-153">Quando non è specificato alcun percorso, viene usato solo l'URL specificato nella definizione del servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="11cb9-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="11cb9-154">index</span><span class="sxs-lookup"><span data-stu-id="11cb9-154">index</span></span> |<span data-ttu-id="11cb9-155">Indice della tabella nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="11cb9-155">The index of the table in the resource.</span></span> <span data-ttu-id="11cb9-156">Per i passaggi per ottenere l'indice di una tabella in una pagina HTML, vedere la sezione [Ottenere l'indice di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) .</span><span class="sxs-lookup"><span data-stu-id="11cb9-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="11cb9-157">Sì</span><span class="sxs-lookup"><span data-stu-id="11cb9-157">Yes</span></span> |

<span data-ttu-id="11cb9-158">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="11cb9-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="11cb9-159">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="11cb9-159">Copy activity properties</span></span>
<span data-ttu-id="11cb9-160">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="11cb9-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="11cb9-161">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="11cb9-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="11cb9-162">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="11cb9-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="11cb9-163">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="11cb9-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="11cb9-164">Quando l'origine nell'attività di copia è di tipo **WebSource**non sono attualmente supportate altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="11cb9-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="11cb9-165">Esempio JSON: Copiare dati da una tabella Web a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="11cb9-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="11cb9-166">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="11cb9-166">The following sample shows:</span></span>

1. <span data-ttu-id="11cb9-167">Un servizio collegato di tipo [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="11cb9-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="11cb9-168">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="11cb9-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="11cb9-169">Un [set di dati](data-factory-create-datasets.md) di input di tipo [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="11cb9-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="11cb9-170">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="11cb9-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="11cb9-171">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="11cb9-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="11cb9-172">Nell'esempio i dati vengono copiati da una tabella Web a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="11cb9-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="11cb9-173">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="11cb9-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="11cb9-174">Questo esempio illustra come copiare dati da una tabella Web a un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="11cb9-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="11cb9-175">Tuttavia, i dati possono essere copiati direttamente in uno qualsiasi dei sink indicati nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="11cb9-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="11cb9-176">**Servizio collegato Web** : questo esempio usa il servizio collegato Web con l'autenticazione anonima.</span><span class="sxs-lookup"><span data-stu-id="11cb9-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="11cb9-177">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato Web](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="11cb9-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="11cb9-178">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="11cb9-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="11cb9-179">**Set di dati di input WebTable** Impostando **external** su **true**, si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="11cb9-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="11cb9-180">Per i passaggi per ottenere l'indice di una tabella in una pagina HTML, vedere la sezione [Ottenere l'indice di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) .</span><span class="sxs-lookup"><span data-stu-id="11cb9-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="11cb9-181">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="11cb9-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="11cb9-182">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="11cb9-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="11cb9-183">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="11cb9-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="11cb9-184">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="11cb9-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="11cb9-185">Nella definizione JSON della pipeline, il tipo **source** è impostato su **WebSource** e il tipo **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="11cb9-186">Per l'elenco delle proprietà supportate da WebSource, vedere le [proprietà del tipo WebSource](#copy-activity-type-properties) .</span><span class="sxs-lookup"><span data-stu-id="11cb9-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="11cb9-187">Ottenere l'indice di una tabella in una pagina HTML</span><span class="sxs-lookup"><span data-stu-id="11cb9-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="11cb9-188">Avviare **Excel 2016** e passare alla scheda **Dati**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="11cb9-189">Fare clic su **Nuova query** sulla barra degli strumenti, scegliere **Da altre origini** e fare clic su **Da Web**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Menu di Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="11cb9-191">Nella finestra di dialogo **Da Web** immettere l'**URL** che si intende usare nel servizio collegato JSON, ad esempio https://en.wikipedia.org/wiki/, insieme al percorso specificato per il set di dati, ad esempio AFI%27s_100_Years...100_Movies, e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Finestra di dialogo Da Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="11cb9-193">URL usato in questo esempio: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="11cb9-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="11cb9-194">Se viene visualizzata la finestra di dialogo **Accedi a contenuto Web**, selezionare l'**URL** corretto, l'**autenticazione** e fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="11cb9-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Finestra di dialogo Accedi a contenuto Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="11cb9-196">Fare clic su un elemento della **tabella** nella visualizzazione ad albero per visualizzare il contenuto dalla tabella e quindi fare clic su **Modifica** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="11cb9-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Finestra di dialogo Strumento di spostamento](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="11cb9-198">Nella finestra **Editor di query** fare clic sul pulsante **Editor avanzato** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="11cb9-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Pulsante Editor avanzato](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="11cb9-200">Nella finestra di dialogo Editor avanzato il numero accanto a "Source" è l'indice.</span><span class="sxs-lookup"><span data-stu-id="11cb9-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Editor avanzato - Indice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="11cb9-202">Se si usa Excel 2013, per ottenere l'indice usare [Microsoft Power Query per Excel](https://www.microsoft.com/download/details.aspx?id=39379) .</span><span class="sxs-lookup"><span data-stu-id="11cb9-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="11cb9-203">Per informazioni dettagliate, vedere l'articolo [Connettersi a una pagina Web (Power Query)](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) .</span><span class="sxs-lookup"><span data-stu-id="11cb9-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="11cb9-204">I passaggi sono simili se si usa [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="11cb9-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="11cb9-205">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="11cb9-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="11cb9-206">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="11cb9-206">Performance and Tuning</span></span>
<span data-ttu-id="11cb9-207">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="11cb9-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
