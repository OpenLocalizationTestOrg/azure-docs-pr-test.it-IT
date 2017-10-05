---
title: Spostare i dati da Amazon Redshift usando Data Factory | Documentazione Microsoft
description: Informazioni su come spostare i dati da origini Amazon Redshift usando Azure Data Factory.
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
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="acdaa-103">Spostare i dati da Amazon Redshift usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="acdaa-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="acdaa-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="acdaa-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="acdaa-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="acdaa-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="acdaa-106">È possibile copiare dati da Amazon Redshift a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="acdaa-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="acdaa-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="acdaa-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="acdaa-108">Data Factory supporta attualmente lo spostamento di dati da Amazon Redshift ad altri archivi dati, non da altri archivi dati ad Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="acdaa-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acdaa-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="acdaa-109">Prerequisites</span></span>
* <span data-ttu-id="acdaa-110">Se si spostano i dati in un archivio dati locale, installare il [gateway di gestione dati](data-factory-data-management-gateway.md) su un computer locale.</span><span class="sxs-lookup"><span data-stu-id="acdaa-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="acdaa-111">Quindi concedere al gateway di gestione dati (usa l'indirizzo IP della macchina) l'accesso al cluster Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="acdaa-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="acdaa-112">Vedere [Autorizzare l'accesso al cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="acdaa-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="acdaa-113">Se si spostano dati in un archivio dati di Azure, vedere [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) (Intervalli IP del centro dati di Azure) per gli intervalli di indirizzi IP ed SQL di calcolo usati dai data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="acdaa-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="acdaa-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="acdaa-114">Getting started</span></span>
<span data-ttu-id="acdaa-115">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine Amazon Redshift usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="acdaa-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="acdaa-116">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="acdaa-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="acdaa-117">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="acdaa-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="acdaa-118">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="acdaa-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="acdaa-119">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="acdaa-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="acdaa-120">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="acdaa-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="acdaa-121">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="acdaa-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="acdaa-122">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="acdaa-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="acdaa-123">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="acdaa-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="acdaa-124">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="acdaa-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="acdaa-125">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="acdaa-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="acdaa-126">Per un esempio con definizioni JSON per entità di data factory utilizzate per copiare dati da un archivio dati Amazon Redshift, vedere la sezione [Esempio JSON: Copiare dati da Amazon Redshift al BLOB di Azure](#json-example-copy-data-from-amazon-redshift-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="acdaa-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="acdaa-127">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di Amazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="acdaa-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="acdaa-128">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="acdaa-128">Linked service properties</span></span>
<span data-ttu-id="acdaa-129">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="acdaa-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="acdaa-130">Proprietà</span><span class="sxs-lookup"><span data-stu-id="acdaa-130">Property</span></span> | <span data-ttu-id="acdaa-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="acdaa-131">Description</span></span> | <span data-ttu-id="acdaa-132">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="acdaa-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="acdaa-133">type</span><span class="sxs-lookup"><span data-stu-id="acdaa-133">type</span></span> |<span data-ttu-id="acdaa-134">La proprietà type deve essere impostata su: **Amazon Redshift**.</span><span class="sxs-lookup"><span data-stu-id="acdaa-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="acdaa-135">Sì</span><span class="sxs-lookup"><span data-stu-id="acdaa-135">Yes</span></span> |
| <span data-ttu-id="acdaa-136">server</span><span class="sxs-lookup"><span data-stu-id="acdaa-136">server</span></span> |<span data-ttu-id="acdaa-137">Indirizzo IP o nome host del server Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="acdaa-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="acdaa-138">Sì</span><span class="sxs-lookup"><span data-stu-id="acdaa-138">Yes</span></span> |
| <span data-ttu-id="acdaa-139">port</span><span class="sxs-lookup"><span data-stu-id="acdaa-139">port</span></span> |<span data-ttu-id="acdaa-140">Il numero della porta TCP che il server Amazon Redshift usa per ascoltare le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="acdaa-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="acdaa-141">No, valore predefinito: 5439</span><span class="sxs-lookup"><span data-stu-id="acdaa-141">No, default value: 5439</span></span> |
| <span data-ttu-id="acdaa-142">database</span><span class="sxs-lookup"><span data-stu-id="acdaa-142">database</span></span> |<span data-ttu-id="acdaa-143">Nome del database Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="acdaa-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="acdaa-144">Sì</span><span class="sxs-lookup"><span data-stu-id="acdaa-144">Yes</span></span> |
| <span data-ttu-id="acdaa-145">Nome utente</span><span class="sxs-lookup"><span data-stu-id="acdaa-145">username</span></span> |<span data-ttu-id="acdaa-146">Nome dell'utente che ha accesso al database.</span><span class="sxs-lookup"><span data-stu-id="acdaa-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="acdaa-147">Sì</span><span class="sxs-lookup"><span data-stu-id="acdaa-147">Yes</span></span> |
| <span data-ttu-id="acdaa-148">password</span><span class="sxs-lookup"><span data-stu-id="acdaa-148">password</span></span> |<span data-ttu-id="acdaa-149">La password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="acdaa-149">Password for the user account.</span></span> |<span data-ttu-id="acdaa-150">Sì</span><span class="sxs-lookup"><span data-stu-id="acdaa-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="acdaa-151">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="acdaa-151">Dataset properties</span></span>
<span data-ttu-id="acdaa-152">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="acdaa-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="acdaa-153">Le sezioni come struttura, disponibilità e criteri sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="acdaa-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="acdaa-154">La sezione **typeProperties** è diversa per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="acdaa-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="acdaa-155">Offre informazioni sul percorso dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="acdaa-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="acdaa-156">La sezione typeProperties per il set di dati di tipo **RelationalTable** (che comprende il set di dati Amazon Redshift) presenta le proprietà seguenti</span><span class="sxs-lookup"><span data-stu-id="acdaa-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="acdaa-157">Proprietà</span><span class="sxs-lookup"><span data-stu-id="acdaa-157">Property</span></span> | <span data-ttu-id="acdaa-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="acdaa-158">Description</span></span> | <span data-ttu-id="acdaa-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="acdaa-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="acdaa-160">tableName</span><span class="sxs-lookup"><span data-stu-id="acdaa-160">tableName</span></span> |<span data-ttu-id="acdaa-161">Nome della tabella nel database Amazon Redshift a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="acdaa-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="acdaa-162">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="acdaa-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="acdaa-163">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="acdaa-163">Copy activity properties</span></span>
<span data-ttu-id="acdaa-164">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="acdaa-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="acdaa-165">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="acdaa-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="acdaa-166">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="acdaa-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="acdaa-167">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="acdaa-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="acdaa-168">Quando l'origine dell'attività di copia è di tipo **RelationalSource** (che include Amazon Redshift), nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="acdaa-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="acdaa-169">Proprietà</span><span class="sxs-lookup"><span data-stu-id="acdaa-169">Property</span></span> | <span data-ttu-id="acdaa-170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="acdaa-170">Description</span></span> | <span data-ttu-id="acdaa-171">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="acdaa-171">Allowed values</span></span> | <span data-ttu-id="acdaa-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="acdaa-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="acdaa-173">query</span><span class="sxs-lookup"><span data-stu-id="acdaa-173">query</span></span> |<span data-ttu-id="acdaa-174">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="acdaa-174">Use the custom query to read data.</span></span> |<span data-ttu-id="acdaa-175">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="acdaa-175">SQL query string.</span></span> <span data-ttu-id="acdaa-176">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="acdaa-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="acdaa-177">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="acdaa-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="acdaa-178">Esempio JSON: Copiare dati da Amazon Redshift al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="acdaa-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="acdaa-179">Questo esempio illustra come copiare dati da un database Amazon Redshift a un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="acdaa-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="acdaa-180">Tuttavia, i dati possono essere copiati **direttamente** in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="acdaa-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="acdaa-181">L'esempio include le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="acdaa-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="acdaa-182">Un servizio collegato di tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="acdaa-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="acdaa-183">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="acdaa-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="acdaa-184">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="acdaa-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="acdaa-185">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="acdaa-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="acdaa-186">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="acdaa-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="acdaa-187">L'esempio copia i dati dai risultati della query in Amazon Redshift in un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="acdaa-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="acdaa-188">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="acdaa-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="acdaa-189">**Servizio collegato Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="acdaa-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="acdaa-190">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="acdaa-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="acdaa-191">**Set di dati di input Redshift Amazon:**</span><span class="sxs-lookup"><span data-stu-id="acdaa-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="acdaa-192">L'impostazione `"external": true` comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è generato da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="acdaa-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="acdaa-193">Impostare questa proprietà su true in un set di dati di input non generato da un'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="acdaa-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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

<span data-ttu-id="acdaa-194">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="acdaa-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="acdaa-195">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="acdaa-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="acdaa-196">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="acdaa-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="acdaa-197">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="acdaa-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="acdaa-198">**Attività di copia in una pipeline con origine Amazon Redshift (RelationalSource) e sink BLOB.**</span><span class="sxs-lookup"><span data-stu-id="acdaa-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="acdaa-199">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="acdaa-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="acdaa-200">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="acdaa-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="acdaa-201">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="acdaa-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="acdaa-202">Tipo di mappatura di Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="acdaa-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="acdaa-203">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="acdaa-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="acdaa-204">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="acdaa-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="acdaa-205">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="acdaa-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="acdaa-206">Quando si spostano i dati in Amazon Redshift, vengono usati i mapping seguenti dai tipi di Amazon Redshift ai tipi .NET.</span><span class="sxs-lookup"><span data-stu-id="acdaa-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="acdaa-207">Tipo di Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="acdaa-207">Amazon Redshift Type</span></span> | <span data-ttu-id="acdaa-208">Tipo basato su .Net</span><span class="sxs-lookup"><span data-stu-id="acdaa-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="acdaa-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="acdaa-209">SMALLINT</span></span> |<span data-ttu-id="acdaa-210">Int16</span><span class="sxs-lookup"><span data-stu-id="acdaa-210">Int16</span></span> |
| <span data-ttu-id="acdaa-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="acdaa-211">INTEGER</span></span> |<span data-ttu-id="acdaa-212">Int32</span><span class="sxs-lookup"><span data-stu-id="acdaa-212">Int32</span></span> |
| <span data-ttu-id="acdaa-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="acdaa-213">BIGINT</span></span> |<span data-ttu-id="acdaa-214">Int64</span><span class="sxs-lookup"><span data-stu-id="acdaa-214">Int64</span></span> |
| <span data-ttu-id="acdaa-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="acdaa-215">DECIMAL</span></span> |<span data-ttu-id="acdaa-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="acdaa-216">Decimal</span></span> |
| <span data-ttu-id="acdaa-217">REAL</span><span class="sxs-lookup"><span data-stu-id="acdaa-217">REAL</span></span> |<span data-ttu-id="acdaa-218">Single</span><span class="sxs-lookup"><span data-stu-id="acdaa-218">Single</span></span> |
| <span data-ttu-id="acdaa-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="acdaa-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="acdaa-220">Double</span><span class="sxs-lookup"><span data-stu-id="acdaa-220">Double</span></span> |
| <span data-ttu-id="acdaa-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="acdaa-221">BOOLEAN</span></span> |<span data-ttu-id="acdaa-222">String</span><span class="sxs-lookup"><span data-stu-id="acdaa-222">String</span></span> |
| <span data-ttu-id="acdaa-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="acdaa-223">CHAR</span></span> |<span data-ttu-id="acdaa-224">String</span><span class="sxs-lookup"><span data-stu-id="acdaa-224">String</span></span> |
| <span data-ttu-id="acdaa-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="acdaa-225">VARCHAR</span></span> |<span data-ttu-id="acdaa-226">String</span><span class="sxs-lookup"><span data-stu-id="acdaa-226">String</span></span> |
| <span data-ttu-id="acdaa-227">DATE</span><span class="sxs-lookup"><span data-stu-id="acdaa-227">DATE</span></span> |<span data-ttu-id="acdaa-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="acdaa-228">DateTime</span></span> |
| <span data-ttu-id="acdaa-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="acdaa-229">TIMESTAMP</span></span> |<span data-ttu-id="acdaa-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="acdaa-230">DateTime</span></span> |
| <span data-ttu-id="acdaa-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="acdaa-231">TEXT</span></span> |<span data-ttu-id="acdaa-232">String</span><span class="sxs-lookup"><span data-stu-id="acdaa-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="acdaa-233">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="acdaa-233">Map source to sink columns</span></span>
<span data-ttu-id="acdaa-234">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="acdaa-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="acdaa-235">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="acdaa-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="acdaa-236">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="acdaa-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="acdaa-237">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="acdaa-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="acdaa-238">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="acdaa-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="acdaa-239">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="acdaa-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="acdaa-240">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="acdaa-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="acdaa-241">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="acdaa-241">Performance and Tuning</span></span>
<span data-ttu-id="acdaa-242">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="acdaa-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acdaa-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acdaa-243">Next Steps</span></span>
<span data-ttu-id="acdaa-244">Vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="acdaa-244">See the following articles:</span></span>

* <span data-ttu-id="acdaa-245">[Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="acdaa-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
