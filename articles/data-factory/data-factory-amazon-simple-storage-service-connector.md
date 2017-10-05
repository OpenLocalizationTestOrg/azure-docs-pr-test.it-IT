---
title: Spostare i dati da Amazon Simple Storage Service usando Data Factory | Microsoft Docs
description: Informazioni su come spostare i dati da Amazon Simple Storage Service (S3) usando Azure Data Factory.
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
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="c7145-103">Spostare i dati da Amazon Simple Storage Service usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c7145-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="c7145-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="c7145-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="c7145-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="c7145-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c7145-106">È possibile copiare dati da Amazon S3 a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="c7145-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="c7145-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c7145-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c7145-108">Data Factory supporta attualmente solo lo spostamento di dati da Amazon S3 ad altri archivi dati, non da altri archivi dati ad Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="c7145-109">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="c7145-109">Required permissions</span></span>
<span data-ttu-id="c7145-110">Per copiare i dati da Amazon S3, assicurarsi di avere le autorizzazioni indicate di seguito:</span><span class="sxs-lookup"><span data-stu-id="c7145-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="c7145-111">`s3:GetObject` e `s3:GetObjectVersion` per le operazioni di oggetto Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="c7145-112">`s3:ListBucket` per le operazioni di bucket Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="c7145-113">Se si usa la copia guidata di Data Factory, è necessario anche `s3:ListAllMyBuckets`.</span><span class="sxs-lookup"><span data-stu-id="c7145-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="c7145-114">Per informazioni dettagliate sull'elenco completo delle autorizzazioni di Amazon S3 con tutti i dettagli in [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html) (Specificare le autorizzazioni in un criterio).</span><span class="sxs-lookup"><span data-stu-id="c7145-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c7145-115">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c7145-115">Getting started</span></span>
<span data-ttu-id="c7145-116">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine Amazon S3 usando diversi strumenti o API.</span><span class="sxs-lookup"><span data-stu-id="c7145-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="c7145-117">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="c7145-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c7145-118">Per una procedura dettagliata, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="c7145-119">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="c7145-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c7145-120">Per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="c7145-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="c7145-121">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="c7145-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c7145-122">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c7145-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c7145-123">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="c7145-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="c7145-124">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="c7145-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="c7145-125">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c7145-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c7145-126">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c7145-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="c7145-127">Per un esempio con definizioni JSON per entità di Data factory usate per copiare dati da un archivio dati Amazon S3, vedere la sezione [Esempio JSON: copiare dati da Amazon S3 al BLOB di Azure](#json-example-copy-data-from-amazon-s3-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c7145-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="c7145-128">Per informazioni dettagliate sui formati di compressione e i file supportati per l'attività di copia, vedere [Formati di compressione e file in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="c7145-129">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di Data factory specifiche di Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c7145-130">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="c7145-130">Linked service properties</span></span>
<span data-ttu-id="c7145-131">Un servizio collegato collega un archivio dati a una data factory.</span><span class="sxs-lookup"><span data-stu-id="c7145-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="c7145-132">Viene creato un servizio collegato di tipo **AwsAccessKey** per collegare l'archivio dati Amazon S3 alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c7145-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="c7145-133">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato Amazon S3 (AwsAccessKey).</span><span class="sxs-lookup"><span data-stu-id="c7145-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="c7145-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c7145-134">Property</span></span> | <span data-ttu-id="c7145-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7145-135">Description</span></span> | <span data-ttu-id="c7145-136">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="c7145-136">Allowed values</span></span> | <span data-ttu-id="c7145-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c7145-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c7145-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="c7145-138">accessKeyID</span></span> |<span data-ttu-id="c7145-139">ID della chiave di accesso segreta.</span><span class="sxs-lookup"><span data-stu-id="c7145-139">ID of the secret access key.</span></span> |<span data-ttu-id="c7145-140">string</span><span class="sxs-lookup"><span data-stu-id="c7145-140">string</span></span> |<span data-ttu-id="c7145-141">Sì</span><span class="sxs-lookup"><span data-stu-id="c7145-141">Yes</span></span> |
| <span data-ttu-id="c7145-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="c7145-142">secretAccessKey</span></span> |<span data-ttu-id="c7145-143">La stessa chiave di accesso segreta.</span><span class="sxs-lookup"><span data-stu-id="c7145-143">The secret access key itself.</span></span> |<span data-ttu-id="c7145-144">La stringa segreta crittografata</span><span class="sxs-lookup"><span data-stu-id="c7145-144">Encrypted secret string</span></span> |<span data-ttu-id="c7145-145">Sì</span><span class="sxs-lookup"><span data-stu-id="c7145-145">Yes</span></span> |

<span data-ttu-id="c7145-146">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="c7145-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="c7145-147">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="c7145-147">Dataset properties</span></span>
<span data-ttu-id="c7145-148">Per specificare un set di dati per rappresentare i dati di input in un'archiviazione BLOB di Azure, impostare la proprietà del tipo del set di dati su **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="c7145-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="c7145-149">Impostare la proprietà **linkedServiceName** del set di dati sul nome del servizio collegato Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="c7145-150">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="c7145-151">Le sezioni come struttura, disponibilità e criteri sono simili per tutti i tipi di set di dati, ad esempio database SQL, BLOB di Azure e tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7145-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="c7145-152">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="c7145-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c7145-153">La sezione **typeProperties** per un set di dati di tipo **AmazonS3**, che include il set di dati Amazon S3, presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7145-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="c7145-154">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c7145-154">Property</span></span> | <span data-ttu-id="c7145-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7145-155">Description</span></span> | <span data-ttu-id="c7145-156">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="c7145-156">Allowed values</span></span> | <span data-ttu-id="c7145-157">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c7145-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c7145-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="c7145-158">bucketName</span></span> |<span data-ttu-id="c7145-159">Il nome del bucket S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-159">The S3 bucket name.</span></span> |<span data-ttu-id="c7145-160">string</span><span class="sxs-lookup"><span data-stu-id="c7145-160">String</span></span> |<span data-ttu-id="c7145-161">Sì</span><span class="sxs-lookup"><span data-stu-id="c7145-161">Yes</span></span> |
| <span data-ttu-id="c7145-162">key</span><span class="sxs-lookup"><span data-stu-id="c7145-162">key</span></span> |<span data-ttu-id="c7145-163">La chiave dell'oggetto S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-163">The S3 object key.</span></span> |<span data-ttu-id="c7145-164">string</span><span class="sxs-lookup"><span data-stu-id="c7145-164">String</span></span> |<span data-ttu-id="c7145-165">No</span><span class="sxs-lookup"><span data-stu-id="c7145-165">No</span></span> |
| <span data-ttu-id="c7145-166">prefix</span><span class="sxs-lookup"><span data-stu-id="c7145-166">prefix</span></span> |<span data-ttu-id="c7145-167">Il prefisso per la chiave dell'oggetto S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="c7145-168">Vengono selezionati gli oggetti le cui chiavi iniziano con questo prefisso.</span><span class="sxs-lookup"><span data-stu-id="c7145-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="c7145-169">Si applica solo quando la chiave è vuota.</span><span class="sxs-lookup"><span data-stu-id="c7145-169">Applies only when key is empty.</span></span> |<span data-ttu-id="c7145-170">string</span><span class="sxs-lookup"><span data-stu-id="c7145-170">String</span></span> |<span data-ttu-id="c7145-171">No</span><span class="sxs-lookup"><span data-stu-id="c7145-171">No</span></span> |
| <span data-ttu-id="c7145-172">version</span><span class="sxs-lookup"><span data-stu-id="c7145-172">version</span></span> |<span data-ttu-id="c7145-173">La versione dell'oggetto S3 se è stato abilitato il controllo delle versioni S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="c7145-174">String</span><span class="sxs-lookup"><span data-stu-id="c7145-174">String</span></span> |<span data-ttu-id="c7145-175">No</span><span class="sxs-lookup"><span data-stu-id="c7145-175">No</span></span> |
| <span data-ttu-id="c7145-176">format</span><span class="sxs-lookup"><span data-stu-id="c7145-176">format</span></span> | <span data-ttu-id="c7145-177">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c7145-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c7145-178">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="c7145-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="c7145-179">Per altre informazioni, vedere le sezioni [Formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Formato AVRO](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato OCR](data-factory-supported-file-and-compression-formats.md#orc-format) e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="c7145-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c7145-180">Per copiare i file così come sono tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="c7145-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c7145-181">No</span><span class="sxs-lookup"><span data-stu-id="c7145-181">No</span></span> | |
| <span data-ttu-id="c7145-182">compressione</span><span class="sxs-lookup"><span data-stu-id="c7145-182">compression</span></span> | <span data-ttu-id="c7145-183">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c7145-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c7145-184">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c7145-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c7145-185">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="c7145-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c7145-186">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c7145-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c7145-187">No</span><span class="sxs-lookup"><span data-stu-id="c7145-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="c7145-188">**bucketName + key** specifica la posizione dell'oggetto S3 in cui il bucket è il contenitore radice per gli oggetti S3 e key rappresenta il percorso completo all'oggetto S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="c7145-189">Set di dati di esempio con prefisso</span><span class="sxs-lookup"><span data-stu-id="c7145-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="c7145-190">Set di dati di esempio (con versione)</span><span class="sxs-lookup"><span data-stu-id="c7145-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="c7145-191">Percorsi dinamici per S3</span><span class="sxs-lookup"><span data-stu-id="c7145-191">Dynamic paths for S3</span></span>
<span data-ttu-id="c7145-192">Nell'esempio precedente vengono usati dei valori fissi per le proprietà **key** e **bucketName** nel set di dati Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="c7145-193">È possibile fare in modo che Data Factory calcoli queste proprietà dinamicamente in fase di runtime usando le variabili di sistema, come SliceStart.</span><span class="sxs-lookup"><span data-stu-id="c7145-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="c7145-194">È possibile eseguire la stessa operazione per la proprietà **prefix** di un set di dati di Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c7145-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="c7145-195">Per un elenco delle funzioni e delle variabili, vedere [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="c7145-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c7145-196">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="c7145-196">Copy activity properties</span></span>
<span data-ttu-id="c7145-197">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="c7145-198">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="c7145-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="c7145-199">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="c7145-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c7145-200">Per l'attività di copia, le proprietà variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="c7145-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="c7145-201">Se l'origine nell'attività di copia è di tipo **FileSystemSource**, che comprende Amazon S3, sono disponibili le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="c7145-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="c7145-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c7145-202">Property</span></span> | <span data-ttu-id="c7145-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7145-203">Description</span></span> | <span data-ttu-id="c7145-204">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="c7145-204">Allowed values</span></span> | <span data-ttu-id="c7145-205">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c7145-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c7145-206">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="c7145-206">recursive</span></span> |<span data-ttu-id="c7145-207">Specifica se elencare in modo ricorsivo gli oggetti S3 sotto la directory.</span><span class="sxs-lookup"><span data-stu-id="c7145-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="c7145-208">true/false</span><span class="sxs-lookup"><span data-stu-id="c7145-208">true/false</span></span> |<span data-ttu-id="c7145-209">No</span><span class="sxs-lookup"><span data-stu-id="c7145-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="c7145-210">Esempio JSON: copiare dati da Amazon S3 al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c7145-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="c7145-211">Questo esempio illustra come copiare i dati da Amazon S3 all'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7145-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="c7145-212">I dati possono tuttavia essere copiati direttamente in [uno qualsiasi dei sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c7145-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="c7145-213">L'esempio fornisce le definizioni JSON per le entità di data factory seguenti.</span><span class="sxs-lookup"><span data-stu-id="c7145-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="c7145-214">È possibile usare queste definizioni per creare una pipeline per copiare dati da Amazon S3 a un archivio BLOB mediante il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="c7145-215">Un servizio collegato di tipo [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c7145-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="c7145-216">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c7145-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="c7145-217">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c7145-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="c7145-218">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c7145-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c7145-219">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c7145-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c7145-220">Nell'esempio i dati vengono copiati da Amazon S3 a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="c7145-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="c7145-221">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="c7145-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="c7145-222">Servizio collegato Amazon S3</span><span class="sxs-lookup"><span data-stu-id="c7145-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c7145-223">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c7145-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="c7145-224">Set di dati di input Amazon S3</span><span class="sxs-lookup"><span data-stu-id="c7145-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="c7145-225">Impostando **"external": "true"** si comunica al servizio Data Factory che il set di dati è esterno alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c7145-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="c7145-226">Impostare questa proprietà su true in un set di dati di input non generato da un'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7145-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c7145-227">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c7145-227">Azure Blob output dataset</span></span>

<span data-ttu-id="c7145-228">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="c7145-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c7145-229">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c7145-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c7145-230">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="c7145-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="c7145-231">Attività di copia in una pipeline con un'origine Amazon S3 e un sink BLOB</span><span class="sxs-lookup"><span data-stu-id="c7145-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="c7145-232">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="c7145-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="c7145-233">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **FileSystemSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c7145-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="c7145-234">Per eseguire il mapping dal set di dati di origine alle colonne dal set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7145-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7145-235">Next steps</span></span>
<span data-ttu-id="c7145-236">Vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7145-236">See the following articles:</span></span>

* <span data-ttu-id="c7145-237">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md) .</span><span class="sxs-lookup"><span data-stu-id="c7145-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="c7145-238">Per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia, vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c7145-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
