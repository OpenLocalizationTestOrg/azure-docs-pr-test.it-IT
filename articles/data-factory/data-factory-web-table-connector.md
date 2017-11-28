---
title: aaaMove dati dalla tabella di Web usando Azure Data Factory | Documenti Microsoft
description: Informazioni su come pagine di dati toomove da una tabella in un sito Web usando Azure Data Factory.
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
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="4b446-103">Spostare i dati da un'origine tabella Web con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b446-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="4b446-104">In questo articolo descrive come toouse hello attività di copia dei dati toomove Data Factory di Azure da una tabella in una pagina Web di tooa supportato archivio dati sink.</span><span class="sxs-lookup"><span data-stu-id="4b446-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="4b446-105">In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo che presenta una panoramica generale di spostamento dei dati con l'elenco di attività e hello copia di archivi dati supportata come origine/sink.</span><span class="sxs-lookup"><span data-stu-id="4b446-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="4b446-106">Data factory di attualmente supporta solo lo spostamento dei dati da un server di dati Web tabella tooother Archivia, ma non lo spostamento dei dati da altri dati archivia tooa Web tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4b446-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b446-107">Questo connettore Web attualmente supporta soltanto l'estrazione del contenuto della tabella da una pagina HTML.</span><span class="sxs-lookup"><span data-stu-id="4b446-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="4b446-108">tooretrieve dei dati da un endpoint HTTP/s, utilizzare [connettore HTTP](data-factory-http-connector.md) invece.</span><span class="sxs-lookup"><span data-stu-id="4b446-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4b446-109">introduttiva</span><span class="sxs-lookup"><span data-stu-id="4b446-109">Getting started</span></span>
<span data-ttu-id="4b446-110">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="4b446-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="4b446-111">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="4b446-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4b446-112">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="4b446-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="4b446-113">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="4b446-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4b446-114">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="4b446-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4b446-115">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b446-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4b446-116">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="4b446-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4b446-117">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="4b446-118">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="4b446-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4b446-119">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="4b446-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4b446-120">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4b446-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4b446-121">Per un esempio con le definizioni di JSON per le entità Data Factory toocopy utilizzati dati da una tabella web, vedere [esempio JSON: copiare i dati dalla tabella di Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4b446-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="4b446-122">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che siano utilizzati toodefine Data Factory entità specifiche tooa Web tabella:</span><span class="sxs-lookup"><span data-stu-id="4b446-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4b446-123">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="4b446-123">Linked service properties</span></span>
<span data-ttu-id="4b446-124">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooWeb collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="4b446-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="4b446-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4b446-125">Property</span></span> | <span data-ttu-id="4b446-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4b446-126">Description</span></span> | <span data-ttu-id="4b446-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4b446-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b446-128">type</span><span class="sxs-lookup"><span data-stu-id="4b446-128">type</span></span> |<span data-ttu-id="4b446-129">proprietà di tipo Hello deve essere impostata su: **Web**</span><span class="sxs-lookup"><span data-stu-id="4b446-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="4b446-130">Sì</span><span class="sxs-lookup"><span data-stu-id="4b446-130">Yes</span></span> |
| <span data-ttu-id="4b446-131">Url</span><span class="sxs-lookup"><span data-stu-id="4b446-131">Url</span></span> |<span data-ttu-id="4b446-132">Origine di URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="4b446-132">URL toohello Web source</span></span> |<span data-ttu-id="4b446-133">Sì</span><span class="sxs-lookup"><span data-stu-id="4b446-133">Yes</span></span> |
| <span data-ttu-id="4b446-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="4b446-134">authenticationType</span></span> |<span data-ttu-id="4b446-135">Anonimo.</span><span class="sxs-lookup"><span data-stu-id="4b446-135">Anonymous.</span></span> |<span data-ttu-id="4b446-136">Sì</span><span class="sxs-lookup"><span data-stu-id="4b446-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="4b446-137">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="4b446-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="4b446-138">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="4b446-138">Dataset properties</span></span>
<span data-ttu-id="4b446-139">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="4b446-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4b446-140">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="4b446-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4b446-141">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="4b446-142">sezione Hello typeProperties per set di dati di tipo **tabella Web** ha hello seguenti proprietà</span><span class="sxs-lookup"><span data-stu-id="4b446-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="4b446-143">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4b446-143">Property</span></span> | <span data-ttu-id="4b446-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4b446-144">Description</span></span> | <span data-ttu-id="4b446-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4b446-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b446-146">type</span><span class="sxs-lookup"><span data-stu-id="4b446-146">type</span></span> |<span data-ttu-id="4b446-147">tipo di set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-147">type of hello dataset.</span></span> <span data-ttu-id="4b446-148">deve essere impostato troppo**tabella Web**</span><span class="sxs-lookup"><span data-stu-id="4b446-148">must be set too**WebTable**</span></span> |<span data-ttu-id="4b446-149">Sì</span><span class="sxs-lookup"><span data-stu-id="4b446-149">Yes</span></span> |
| <span data-ttu-id="4b446-150">path</span><span class="sxs-lookup"><span data-stu-id="4b446-150">path</span></span> |<span data-ttu-id="4b446-151">Una risorsa relativa di URL toohello che contiene la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="4b446-152">No.</span><span class="sxs-lookup"><span data-stu-id="4b446-152">No.</span></span> <span data-ttu-id="4b446-153">Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="4b446-154">index</span><span class="sxs-lookup"><span data-stu-id="4b446-154">index</span></span> |<span data-ttu-id="4b446-155">indice di Hello della tabella hello nella risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="4b446-156">Vedere [indice Get di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) sezione per indice toogetting passaggi di una tabella in una pagina HTML.</span><span class="sxs-lookup"><span data-stu-id="4b446-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="4b446-157">Sì</span><span class="sxs-lookup"><span data-stu-id="4b446-157">Yes</span></span> |

<span data-ttu-id="4b446-158">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="4b446-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="4b446-159">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="4b446-159">Copy activity properties</span></span>
<span data-ttu-id="4b446-160">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="4b446-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4b446-161">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="4b446-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4b446-162">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="4b446-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="4b446-163">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="4b446-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4b446-164">Attualmente, quando origine hello in attività di copia è di tipo **WebSource**, non sono supportate proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="4b446-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="4b446-165">Esempio JSON: copiare i dati dalla tabella di Web tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="4b446-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="4b446-166">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="4b446-166">hello following sample shows:</span></span>

1. <span data-ttu-id="4b446-167">Un servizio collegato di tipo [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b446-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="4b446-168">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b446-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4b446-169">Un [set di dati](data-factory-create-datasets.md) di input di tipo [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b446-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="4b446-170">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b446-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4b446-171">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4b446-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4b446-172">esempio Hello copia dati da un tooan tabella Web blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4b446-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="4b446-173">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="4b446-174">Hello seguente esempio mostra come blob di dati di toocopy da un tooan tabella Web Azure.</span><span class="sxs-lookup"><span data-stu-id="4b446-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="4b446-175">Tuttavia, i dati possono essere copiati direttamente tooany di hello sink hello dichiarato nella [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo usando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4b446-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="4b446-176">**Servizio collegato Web** in questo esempio utilizza hello Web collegato del servizio con l'autenticazione anonima.</span><span class="sxs-lookup"><span data-stu-id="4b446-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="4b446-177">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato Web](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="4b446-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="4b446-178">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="4b446-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="4b446-179">**Set di dati della tabella Web input** impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività in hello factory di dati.</span><span class="sxs-lookup"><span data-stu-id="4b446-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="4b446-180">Vedere [indice Get di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) sezione per indice toogetting passaggi di una tabella in una pagina HTML.</span><span class="sxs-lookup"><span data-stu-id="4b446-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="4b446-181">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="4b446-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="4b446-182">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="4b446-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="4b446-183">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="4b446-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="4b446-184">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4b446-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="4b446-185">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**WebSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4b446-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="4b446-186">Vedere [le proprietà del tipo WebSource](#copy-activity-type-properties) per elenco hello delle proprietà supportate da hello WebSource.</span><span class="sxs-lookup"><span data-stu-id="4b446-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

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
        "description": "Copy from a Web table tooan Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="4b446-187">Ottenere l'indice di una tabella in una pagina HTML</span><span class="sxs-lookup"><span data-stu-id="4b446-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="4b446-188">Avviare **Excel 2016** e passare toohello **dati** scheda.</span><span class="sxs-lookup"><span data-stu-id="4b446-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="4b446-189">Fare clic su **nuova Query** sulla barra degli strumenti hello, scegliere troppo**da altre origini** e fare clic su **da Web**.</span><span class="sxs-lookup"><span data-stu-id="4b446-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Menu di Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="4b446-191">In hello **da Web** finestra di dialogo immettere **URL** che verrebbe utilizzato nel collegamento formato JSON del servizio (ad esempio: https://en.wikipedia.org/wiki/) insieme al percorso desiderato per set di dati hello (ad esempio: AFI % 27s_100_Years... 100_Movies), fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b446-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Finestra di dialogo Da Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="4b446-193">URL usato in questo esempio: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="4b446-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="4b446-194">Se viene visualizzato **contenuto Web di accesso** la finestra di dialogo, a destra selezionare hello **URL**, **autenticazione**, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="4b446-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Finestra di dialogo Accedi a contenuto Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="4b446-196">Fare clic su un **tabella** elemento contenuto toosee della visualizzazione albero hello dalla tabella hello e quindi fare clic su **modifica** pulsante nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Finestra di dialogo Strumento di spostamento](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="4b446-198">In hello **Editor di Query** finestra, fare clic su **Editor avanzato** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Pulsante Editor avanzato](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="4b446-200">Nella finestra di dialogo Editor avanzato hello, hello numero accanto troppo "Source" è indice di hello.</span><span class="sxs-lookup"><span data-stu-id="4b446-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Editor avanzato - Indice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="4b446-202">Se si utilizza Excel 2013, utilizzare [Microsoft Power Query per Excel](https://www.microsoft.com/download/details.aspx?id=39379) indice hello tooget.</span><span class="sxs-lookup"><span data-stu-id="4b446-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="4b446-203">Vedere [pagina web di connessione tooa](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="4b446-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="4b446-204">Hello passaggi sono simili se si utilizza [Microsoft Power BI per Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="4b446-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="4b446-205">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4b446-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4b446-206">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="4b446-206">Performance and Tuning</span></span>
<span data-ttu-id="4b446-207">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="4b446-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
