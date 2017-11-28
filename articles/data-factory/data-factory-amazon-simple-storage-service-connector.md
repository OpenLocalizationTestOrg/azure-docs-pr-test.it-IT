---
title: aaaMove dati dal servizio di archiviazione semplice Amazon utilizzando Data Factory | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati dal servizio di archiviazione semplice Amazon (S3) usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="d1944-103">Spostare i dati da Amazon Simple Storage Service usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d1944-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="d1944-104">Questo articolo spiega come hello toouse attività di copia dei dati di Azure Data Factory toomove dal servizio di archiviazione semplice Amazon (S3).</span><span class="sxs-lookup"><span data-stu-id="d1944-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="d1944-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d1944-106">È possibile copiare i dati dall'archivio dati di Amazon S3 tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="d1944-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="d1944-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="d1944-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d1944-108">Data Factory supporta attualmente solo lo spostamento dei dati dagli archivi di dati tooother S3 Amazon, ma non lo spostamento dei dati da altri dati archivia tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d1944-109">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="d1944-109">Required permissions</span></span>
<span data-ttu-id="d1944-110">dati toocopy S3 Amazon, verificare che sia stato concesso hello queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="d1944-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="d1944-111">`s3:GetObject` e `s3:GetObjectVersion` per le operazioni di oggetto Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="d1944-112">`s3:ListBucket` per le operazioni di bucket Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="d1944-113">Se si utilizza Copia guidata di Data Factory, hello `s3:ListAllMyBuckets` è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="d1944-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="d1944-114">Per informazioni dettagliate sull'elenco completo di hello di Amazon S3 autorizzazioni, vedere [che specifica le autorizzazioni in un criterio](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="d1944-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="d1944-115">introduttiva</span><span class="sxs-lookup"><span data-stu-id="d1944-115">Getting started</span></span>
<span data-ttu-id="d1944-116">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine Amazon S3 usando diversi strumenti o API.</span><span class="sxs-lookup"><span data-stu-id="d1944-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="d1944-117">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="d1944-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d1944-118">Per una procedura dettagliata, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="d1944-119">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d1944-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d1944-120">Per istruzioni dettagliate toocreate una pipeline con attività di copia, vedere hello [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="d1944-121">Se si utilizzano strumenti o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1944-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d1944-122">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d1944-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d1944-123">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="d1944-124">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="d1944-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="d1944-125">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d1944-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d1944-126">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d1944-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="d1944-127">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati S3 Amazon, vedere hello [esempio JSON: copiare i dati da Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d1944-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="d1944-128">Per informazioni dettagliate sui formati di compressione e i file supportati per l'attività di copia, vedere [Formati di compressione e file in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="d1944-129">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d1944-130">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="d1944-130">Linked service properties</span></span>
<span data-ttu-id="d1944-131">Un servizio collegato di collegare una data factory tooa archivio di dati.</span><span class="sxs-lookup"><span data-stu-id="d1944-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="d1944-132">Creare un servizio collegato di tipo **AwsAccessKey** toolink data factory di tooyour di archiviare i dati di Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="d1944-133">Hello nella tabella seguente fornisce il servizio di descrizione per JSON elementi specifici tooAmazon S3 (AwsAccessKey) collegati.</span><span class="sxs-lookup"><span data-stu-id="d1944-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="d1944-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d1944-134">Property</span></span> | <span data-ttu-id="d1944-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d1944-135">Description</span></span> | <span data-ttu-id="d1944-136">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d1944-136">Allowed values</span></span> | <span data-ttu-id="d1944-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d1944-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1944-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="d1944-138">accessKeyID</span></span> |<span data-ttu-id="d1944-139">ID della chiave di accesso privata hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-139">ID of hello secret access key.</span></span> |<span data-ttu-id="d1944-140">string</span><span class="sxs-lookup"><span data-stu-id="d1944-140">string</span></span> |<span data-ttu-id="d1944-141">Sì</span><span class="sxs-lookup"><span data-stu-id="d1944-141">Yes</span></span> |
| <span data-ttu-id="d1944-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="d1944-142">secretAccessKey</span></span> |<span data-ttu-id="d1944-143">chiave di accesso per i segreti Hello stessa.</span><span class="sxs-lookup"><span data-stu-id="d1944-143">hello secret access key itself.</span></span> |<span data-ttu-id="d1944-144">La stringa segreta crittografata</span><span class="sxs-lookup"><span data-stu-id="d1944-144">Encrypted secret string</span></span> |<span data-ttu-id="d1944-145">Sì</span><span class="sxs-lookup"><span data-stu-id="d1944-145">Yes</span></span> |

<span data-ttu-id="d1944-146">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="d1944-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d1944-147">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="d1944-147">Dataset properties</span></span>
<span data-ttu-id="d1944-148">toospecify toorepresent un set di dati di input troppo dati nell'archiviazione Blob di Azure, set di proprietà di tipo hello del set di dati hello**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="d1944-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="d1944-149">Set hello **linkedServiceName** servizio collegato di proprietà del nome di toohello hello set di dati di hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="d1944-150">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="d1944-151">Le sezioni come struttura, disponibilità e criteri sono simili per tutti i tipi di set di dati, ad esempio database SQL, BLOB di Azure e tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1944-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="d1944-152">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d1944-153">Hello **typeProperties** sezione per un set di dati di tipo **AmazonS3** (che include set di dati hello Amazon S3) ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1944-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="d1944-154">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d1944-154">Property</span></span> | <span data-ttu-id="d1944-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d1944-155">Description</span></span> | <span data-ttu-id="d1944-156">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d1944-156">Allowed values</span></span> | <span data-ttu-id="d1944-157">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d1944-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1944-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="d1944-158">bucketName</span></span> |<span data-ttu-id="d1944-159">nome di bucket Hello S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-159">hello S3 bucket name.</span></span> |<span data-ttu-id="d1944-160">String</span><span class="sxs-lookup"><span data-stu-id="d1944-160">String</span></span> |<span data-ttu-id="d1944-161">Sì</span><span class="sxs-lookup"><span data-stu-id="d1944-161">Yes</span></span> |
| <span data-ttu-id="d1944-162">key</span><span class="sxs-lookup"><span data-stu-id="d1944-162">key</span></span> |<span data-ttu-id="d1944-163">chiave dell'oggetto Hello S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-163">hello S3 object key.</span></span> |<span data-ttu-id="d1944-164">String</span><span class="sxs-lookup"><span data-stu-id="d1944-164">String</span></span> |<span data-ttu-id="d1944-165">No</span><span class="sxs-lookup"><span data-stu-id="d1944-165">No</span></span> |
| <span data-ttu-id="d1944-166">prefix</span><span class="sxs-lookup"><span data-stu-id="d1944-166">prefix</span></span> |<span data-ttu-id="d1944-167">Prefisso per la chiave dell'oggetto hello S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="d1944-168">Vengono selezionati gli oggetti le cui chiavi iniziano con questo prefisso.</span><span class="sxs-lookup"><span data-stu-id="d1944-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="d1944-169">Si applica solo quando la chiave è vuota.</span><span class="sxs-lookup"><span data-stu-id="d1944-169">Applies only when key is empty.</span></span> |<span data-ttu-id="d1944-170">string</span><span class="sxs-lookup"><span data-stu-id="d1944-170">String</span></span> |<span data-ttu-id="d1944-171">No</span><span class="sxs-lookup"><span data-stu-id="d1944-171">No</span></span> |
| <span data-ttu-id="d1944-172">version</span><span class="sxs-lookup"><span data-stu-id="d1944-172">version</span></span> |<span data-ttu-id="d1944-173">versione di Hello dell'oggetto hello S3, se è abilitato il controllo delle versioni S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="d1944-174">String</span><span class="sxs-lookup"><span data-stu-id="d1944-174">String</span></span> |<span data-ttu-id="d1944-175">No</span><span class="sxs-lookup"><span data-stu-id="d1944-175">No</span></span> |
| <span data-ttu-id="d1944-176">format</span><span class="sxs-lookup"><span data-stu-id="d1944-176">format</span></span> | <span data-ttu-id="d1944-177">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d1944-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d1944-178">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="d1944-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d1944-179">Per ulteriori informazioni, vedere hello [formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) sezioni.</span><span class="sxs-lookup"><span data-stu-id="d1944-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d1944-180">Se si desidera che il file toocopy come-tra basate su file archivi (copia binaria), skip hello formato sezione in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="d1944-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d1944-181">No</span><span class="sxs-lookup"><span data-stu-id="d1944-181">No</span></span> | |
| <span data-ttu-id="d1944-182">compressione</span><span class="sxs-lookup"><span data-stu-id="d1944-182">compression</span></span> | <span data-ttu-id="d1944-183">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d1944-184">tipi di Hello supportato sono: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d1944-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d1944-185">livelli di Hello supportato sono: **ottimale** e **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="d1944-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d1944-186">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d1944-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d1944-187">No</span><span class="sxs-lookup"><span data-stu-id="d1944-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="d1944-188">**bucketName + tasto** specifica hello percorso dell'oggetto hello S3, dove è il contenitore radice hello per gli oggetti S3 e key oggetto toohello S3 percorso completo di hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="d1944-189">Set di dati di esempio con prefisso</span><span class="sxs-lookup"><span data-stu-id="d1944-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="d1944-190">Set di dati di esempio (con versione)</span><span class="sxs-lookup"><span data-stu-id="d1944-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="d1944-191">Percorsi dinamici per S3</span><span class="sxs-lookup"><span data-stu-id="d1944-191">Dynamic paths for S3</span></span>
<span data-ttu-id="d1944-192">Hello esempio precedente Usa valori fissi per hello **chiave** e **bucketName** proprietà nel set di dati hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="d1944-193">È possibile fare in modo che Data Factory calcoli queste proprietà dinamicamente in fase di runtime usando le variabili di sistema, come SliceStart.</span><span class="sxs-lookup"><span data-stu-id="d1944-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="d1944-194">È possibile eseguire stesso hello per hello **prefisso** proprietà di un set di dati di Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d1944-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="d1944-195">Per un elenco delle funzioni e delle variabili, vedere [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="d1944-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d1944-196">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="d1944-196">Copy activity properties</span></span>
<span data-ttu-id="d1944-197">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="d1944-198">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="d1944-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="d1944-199">Le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="d1944-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d1944-200">Per attività di copia hello, le proprietà variano a seconda di hello tipi di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="d1944-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="d1944-201">Quando un'origine in attività di copia hello è di tipo **FileSystemSource** (che include Amazon S3), hello seguenti proprietà è disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="d1944-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="d1944-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d1944-202">Property</span></span> | <span data-ttu-id="d1944-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d1944-203">Description</span></span> | <span data-ttu-id="d1944-204">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d1944-204">Allowed values</span></span> | <span data-ttu-id="d1944-205">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d1944-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1944-206">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="d1944-206">recursive</span></span> |<span data-ttu-id="d1944-207">Specifica se l'elenco toorecursively S3 oggetti nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="d1944-208">true/false</span><span class="sxs-lookup"><span data-stu-id="d1944-208">true/false</span></span> |<span data-ttu-id="d1944-209">No</span><span class="sxs-lookup"><span data-stu-id="d1944-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="d1944-210">Esempio JSON: copiare i dati da Amazon S3 tooAzure nell'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="d1944-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="d1944-211">Questo esempio viene illustrato come dati toocopy da Amazon S3 tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1944-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="d1944-212">Tuttavia, dati possono essere copiati direttamente troppo[uno qualsiasi dei sink hello supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite attività di copia hello in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d1944-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="d1944-213">esempio Hello fornisce definizioni di JSON per hello seguenti entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d1944-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="d1944-214">È possibile utilizzare questi toocreate definizioni una pipeline di dati dall'archivio tooBlob S3 Amazon, toocopy utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="d1944-215">Un servizio collegato di tipo [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d1944-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="d1944-216">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d1944-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d1944-217">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d1944-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="d1944-218">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d1944-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d1944-219">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d1944-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d1944-220">esempio Hello copia dati da Amazon S3 tooan blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d1944-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="d1944-221">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="d1944-222">Servizio collegato Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d1944-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="d1944-223">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d1944-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="d1944-224">Set di dati di input Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d1944-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="d1944-225">Impostazione **"external": true** informa servizio Data Factory hello di set di dati hello è data factory di toohello esterno.</span><span class="sxs-lookup"><span data-stu-id="d1944-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="d1944-226">Impostare tootrue questa proprietà su un set di dati di input che non è stato generato da un'attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="d1944-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d1944-227">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d1944-227">Azure Blob output dataset</span></span>

<span data-ttu-id="d1944-228">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="d1944-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d1944-229">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="d1944-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d1944-230">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="d1944-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="d1944-231">Attività di copia in una pipeline con un'origine Amazon S3 e un sink BLOB</span><span class="sxs-lookup"><span data-stu-id="d1944-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="d1944-232">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d1944-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="d1944-233">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource**, e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d1944-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="d1944-234">vedere toomap colonne da un toocolumns di set di dati di origine da un set di dati sink [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d1944-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1944-235">Next steps</span></span>
<span data-ttu-id="d1944-236">Vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="d1944-236">See hello following articles:</span></span>

* <span data-ttu-id="d1944-237">toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento (attività di copia) dei dati in Data Factory e toooptimize modi diversi, vedere hello [copiare ottimizzazione Guida e alle prestazioni di attività](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="d1944-238">Per istruzioni dettagliate per la creazione di una pipeline con attività di copia, vedere hello [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d1944-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
