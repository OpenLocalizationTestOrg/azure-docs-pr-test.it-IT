---
title: Copiare dati da/in Azure SQL Data Warehouse | Microsoft Docs
description: Informazioni su come copiare dati da e in Azure SQL Data Warehouse tramite Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="a0c97-103">Copiare dati da e in Azure SQL Data Warehouse tramite Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a0c97-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="a0c97-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a0c97-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a0c97-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="a0c97-106">Per ottenere prestazioni ottimali, usare PolyBase per caricare i dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a0c97-107">Vedere la sezione [Usare PolyBase per caricare dati in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="a0c97-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="a0c97-108">Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="a0c97-109">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="a0c97-109">Supported scenarios</span></span>
<span data-ttu-id="a0c97-110">È possibile copiare i dati **da Azure SQL Data Warehouse** negli archivi di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="a0c97-111">È possibile copiare i dati dagli archivi dati seguenti **ad Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="a0c97-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="a0c97-112">Quando si copiano dati da SQL Server o da Database SQL di Azure in SQL Data Warehouse, se la tabella non esiste nell'archivio di destinazione, Data Factory la crea automaticamente in SQL Data Warehouse usando lo schema della tabella nell'archivio dati di origine.</span><span class="sxs-lookup"><span data-stu-id="a0c97-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="a0c97-113">Per informazioni dettagliate vedere [Creazione automatica della tabella](#auto-table-creation).</span><span class="sxs-lookup"><span data-stu-id="a0c97-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="a0c97-114">Tipo di autenticazione supportato</span><span class="sxs-lookup"><span data-stu-id="a0c97-114">Supported authentication type</span></span>
<span data-ttu-id="a0c97-115">È supportato il connettore Azure SQL Data Warehouse per l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="a0c97-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a0c97-116">Introduzione</span><span class="sxs-lookup"><span data-stu-id="a0c97-116">Getting started</span></span>
<span data-ttu-id="a0c97-117">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un Azure SQL Data Warehouse usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="a0c97-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="a0c97-118">Il modo più semplice di creare una pipeline che copia i dati in/da Azure SQL Data Warehouse consiste nell'usare la procedura Copia di dati guidata.</span><span class="sxs-lookup"><span data-stu-id="a0c97-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="a0c97-119">Vedere [Esercitazione: Caricare i dati in SQL Data Warehouse con Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) per una procedura dettagliata rapida per creare una pipeline usando la procedura guidata Copia dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a0c97-120">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a0c97-121">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a0c97-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="a0c97-122">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="a0c97-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="a0c97-123">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-123">Create a **data factory**.</span></span> <span data-ttu-id="a0c97-124">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="a0c97-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="a0c97-125">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="a0c97-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="a0c97-126">Ad esempio, se si copiano i dati da un'archiviazione BLOB di Azure in Azure SQL Data Warehouse si creano due servizi collegati per collegare l'account di archiviazione di Azure e Azure SQL Data Warehouse alla data factory.</span><span class="sxs-lookup"><span data-stu-id="a0c97-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="a0c97-127">Per le proprietà del servizio collegato specifiche per Azure SQL Data Warehouse, vedere la sezione sulle [proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="a0c97-128">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="a0c97-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="a0c97-129">Nell'esempio citato nel passaggio precedente, si crea un set di dati per specificare un contenitore BLOB e la cartella che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="a0c97-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="a0c97-130">Si crea anche un altro set di dati per specificare la tabella SQL in Azure SQL Data Warehouse che contiene i dati copiati dall'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="a0c97-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="a0c97-131">Per le proprietà del set di dati specifiche per Azure SQL Data Warehouse, vedere la sezione sulle [proprietà del set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="a0c97-132">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="a0c97-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="a0c97-133">Nell'esempio indicato in precedenza si usa BlobSource come origine e SqlDWSink come sink per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a0c97-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="a0c97-134">Analogamente, se si esegue la copia da Azure SQL Data Warehouse nell'archiviazione BLOB di Azure, si usa SqlDWSource e BlobSink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a0c97-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="a0c97-135">Per le proprietà dell'attività di copia specifiche per Azure SQL Data Warehouse, vedere la sezione sulle [proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="a0c97-136">Per informazioni dettagliate su come usare un archivio dati come origine o come sink, fare clic sul collegamento nella sezione precedente per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="a0c97-137">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a0c97-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a0c97-138">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="a0c97-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a0c97-139">Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso un Azure SQL Data Warehouse, vedere la sezione degli [esempi JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a0c97-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="a0c97-140">Le sezioni seguenti riportano le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="a0c97-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a0c97-141">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="a0c97-141">Linked service properties</span></span>
<span data-ttu-id="a0c97-142">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="a0c97-143">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a0c97-143">Property</span></span> | <span data-ttu-id="a0c97-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a0c97-144">Description</span></span> | <span data-ttu-id="a0c97-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a0c97-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0c97-146">type</span><span class="sxs-lookup"><span data-stu-id="a0c97-146">type</span></span> |<span data-ttu-id="a0c97-147">La proprietà del tipo deve essere impostata su: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="a0c97-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="a0c97-148">Sì</span><span class="sxs-lookup"><span data-stu-id="a0c97-148">Yes</span></span> |
| <span data-ttu-id="a0c97-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="a0c97-149">connectionString</span></span> |<span data-ttu-id="a0c97-150">Specificare le informazioni necessarie per connettersi all'istanza di Azure SQL Data Warehouse per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="a0c97-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="a0c97-151">È supportata solo l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="a0c97-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="a0c97-152">Sì</span><span class="sxs-lookup"><span data-stu-id="a0c97-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a0c97-153">Configurare il [firewall del database SQL di Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e il server di database in modo da [consentire ai servizi di Azure di accedere al server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="a0c97-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="a0c97-154">Se si copiano dati in Azure SQL Data Warehouse dall'esterno di Azure e da origini dati locali con gateway di data factory, configurare anche un intervallo di indirizzi IP appropriato per il computer che invia dati ad Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="a0c97-155">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="a0c97-155">Dataset properties</span></span>
<span data-ttu-id="a0c97-156">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a0c97-157">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="a0c97-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a0c97-158">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a0c97-159">La sezione **typeProperties** per il set di dati di tipo **AzureSqlDWTable** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="a0c97-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a0c97-160">Property</span></span> | <span data-ttu-id="a0c97-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a0c97-161">Description</span></span> | <span data-ttu-id="a0c97-162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a0c97-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0c97-163">tableName</span><span class="sxs-lookup"><span data-stu-id="a0c97-163">tableName</span></span> |<span data-ttu-id="a0c97-164">Nome della tabella o della visualizzazione nell'istanza del database SQL Data Warehouse di Azure a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="a0c97-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="a0c97-165">Sì</span><span class="sxs-lookup"><span data-stu-id="a0c97-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a0c97-166">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="a0c97-166">Copy activity properties</span></span>
<span data-ttu-id="a0c97-167">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a0c97-168">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="a0c97-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="a0c97-169">L'attività di copia accetta solo un input e produce solo un output.</span><span class="sxs-lookup"><span data-stu-id="a0c97-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="a0c97-170">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="a0c97-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="a0c97-171">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="a0c97-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="a0c97-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="a0c97-172">SqlDWSource</span></span>
<span data-ttu-id="a0c97-173">In caso di origine di tipo **SqlDWSource**, nella sezione **typeProperties** sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="a0c97-174">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a0c97-174">Property</span></span> | <span data-ttu-id="a0c97-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a0c97-175">Description</span></span> | <span data-ttu-id="a0c97-176">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="a0c97-176">Allowed values</span></span> | <span data-ttu-id="a0c97-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a0c97-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a0c97-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="a0c97-178">sqlReaderQuery</span></span> |<span data-ttu-id="a0c97-179">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-179">Use the custom query to read data.</span></span> |<span data-ttu-id="a0c97-180">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="a0c97-180">SQL query string.</span></span> <span data-ttu-id="a0c97-181">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="a0c97-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="a0c97-182">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-182">No</span></span> |
| <span data-ttu-id="a0c97-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="a0c97-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="a0c97-184">Nome della stored procedure che legge i dati dalla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="a0c97-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="a0c97-185">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-185">Name of the stored procedure.</span></span> <span data-ttu-id="a0c97-186">L'ultima istruzione SQL deve essere un'istruzione SELECT nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="a0c97-187">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-187">No</span></span> |
| <span data-ttu-id="a0c97-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="a0c97-188">storedProcedureParameters</span></span> |<span data-ttu-id="a0c97-189">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="a0c97-190">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="a0c97-190">Name/value pairs.</span></span> <span data-ttu-id="a0c97-191">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="a0c97-192">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-192">No</span></span> |

<span data-ttu-id="a0c97-193">Se la proprietà **sqlReaderQuery** è specificata per SqlDWSource, l'attività di copia esegue questa query nell'origine SQL Data Warehouse di Azure per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="a0c97-194">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="a0c97-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="a0c97-195">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura del set di dati JSON vengono usate per compilare una query da eseguire su Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a0c97-196">Esempio: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="a0c97-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="a0c97-197">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="a0c97-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="a0c97-198">Esempio SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="a0c97-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="a0c97-199">**Definizione della stored procedure:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-199">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="a0c97-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="a0c97-200">SqlDWSink</span></span>
<span data-ttu-id="a0c97-201">**SqlDWSink** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="a0c97-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a0c97-202">Property</span></span> | <span data-ttu-id="a0c97-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a0c97-203">Description</span></span> | <span data-ttu-id="a0c97-204">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="a0c97-204">Allowed values</span></span> | <span data-ttu-id="a0c97-205">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a0c97-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a0c97-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="a0c97-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="a0c97-207">Specificare una query da eseguire nell'attività di copia per pulire i dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="a0c97-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="a0c97-208">Per informazioni dettagliate, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="a0c97-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="a0c97-209">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="a0c97-209">A query statement.</span></span> |<span data-ttu-id="a0c97-210">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-210">No</span></span> |
| <span data-ttu-id="a0c97-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="a0c97-211">allowPolyBase</span></span> |<span data-ttu-id="a0c97-212">Indica se usare PolyBase, quando applicabile, invece del meccanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="a0c97-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="a0c97-213">**L'uso di PolyBase è il modo consigliato per caricare dati in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="a0c97-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="a0c97-214">Per informazioni su vincoli e dettagli, vedere la sezione [Usare PolyBase per caricare dati in Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) .</span><span class="sxs-lookup"><span data-stu-id="a0c97-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="a0c97-215">True </span><span class="sxs-lookup"><span data-stu-id="a0c97-215">True</span></span> <br/><span data-ttu-id="a0c97-216">False (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="a0c97-216">False (default)</span></span> |<span data-ttu-id="a0c97-217">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-217">No</span></span> |
| <span data-ttu-id="a0c97-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="a0c97-218">polyBaseSettings</span></span> |<span data-ttu-id="a0c97-219">Gruppo di proprietà che è possibile specificare quando la proprietà **allowPolybase** è impostata su **true**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="a0c97-220">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-220">No</span></span> |
| <span data-ttu-id="a0c97-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="a0c97-221">rejectValue</span></span> |<span data-ttu-id="a0c97-222">Specifica il numero o la percentuale di righe che è possibile rifiutare prima che la query abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a0c97-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="a0c97-223">Per altre informazioni sulle opzioni di rifiuto di PolyBase, vedere la sezione **Arguments** (Argomenti) in [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a0c97-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="a0c97-224">0 (impostazione predefinita), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="a0c97-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="a0c97-225">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-225">No</span></span> |
| <span data-ttu-id="a0c97-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="a0c97-226">rejectType</span></span> |<span data-ttu-id="a0c97-227">Indica se l'opzione rejectValue viene specificata come valore letterale o come percentuale.</span><span class="sxs-lookup"><span data-stu-id="a0c97-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="a0c97-228">Value (impostazione predefinita), Percentage</span><span class="sxs-lookup"><span data-stu-id="a0c97-228">Value (default), Percentage</span></span> |<span data-ttu-id="a0c97-229">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-229">No</span></span> |
| <span data-ttu-id="a0c97-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="a0c97-230">rejectSampleValue</span></span> |<span data-ttu-id="a0c97-231">Determina il numero di righe da recuperare prima che PolyBase ricalcoli la percentuale di righe rifiutate.</span><span class="sxs-lookup"><span data-stu-id="a0c97-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="a0c97-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="a0c97-232">1, 2, …</span></span> |<span data-ttu-id="a0c97-233">Sì se **rejectType** è **percentage**</span><span class="sxs-lookup"><span data-stu-id="a0c97-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="a0c97-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="a0c97-234">useTypeDefault</span></span> |<span data-ttu-id="a0c97-235">Specifica come gestire i valori mancanti nei file con testo delimitato quando PolyBase recupera dati dal file di testo.</span><span class="sxs-lookup"><span data-stu-id="a0c97-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="a0c97-236">Per altre informazioni su questa proprietà, vedere la sezione Arguments (Argomenti) in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0c97-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="a0c97-237">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="a0c97-237">True, False (default)</span></span> |<span data-ttu-id="a0c97-238">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-238">No</span></span> |
| <span data-ttu-id="a0c97-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="a0c97-239">writeBatchSize</span></span> |<span data-ttu-id="a0c97-240">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="a0c97-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="a0c97-241">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="a0c97-241">Integer (number of rows)</span></span> |<span data-ttu-id="a0c97-242">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-242">No (default: 10000)</span></span> |
| <span data-ttu-id="a0c97-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="a0c97-243">writeBatchTimeout</span></span> |<span data-ttu-id="a0c97-244">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="a0c97-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="a0c97-245">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="a0c97-245">timespan</span></span><br/><br/> <span data-ttu-id="a0c97-246">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="a0c97-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="a0c97-247">No</span><span class="sxs-lookup"><span data-stu-id="a0c97-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="a0c97-248">Esempio SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="a0c97-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="a0c97-249">Usare PolyBase per caricare dati in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a0c97-250">**[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** consente di caricare con efficacia grandi quantità di dati in Azure SQL Data Warehouse con una velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="a0c97-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="a0c97-251">L'uso di PolyBase consente un miglioramento significativo della velocità effettiva rispetto al meccanismo BULKINSERT predefinito.</span><span class="sxs-lookup"><span data-stu-id="a0c97-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="a0c97-252">Vedere [Copiare il numero di riferimento prestazioni](data-factory-copy-activity-performance.md#performance-reference) con il confronto dettagliato.</span><span class="sxs-lookup"><span data-stu-id="a0c97-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="a0c97-253">Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="a0c97-254">Se il formato dei dati di origine è **BLOB di Azure o Azure Data Lake Store** e compatibile con PolyBase, è possibile eseguire la copia direttamente in Azure SQL Data Warehouse usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="a0c97-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="a0c97-255">Vedere **[Copia diretta tramite PolyBase](#direct-copy-using-polybase)** con i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="a0c97-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="a0c97-256">Se l'archivio e il formato dei dati di origine non sono supportati in origine da PolyBase, è possibile usare la funzione **[copia di staging tramite PolyBase](#staged-copy-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="a0c97-257">Viene inoltre generata una migliore velocità effettiva tramite la conversione automatica dei dati nel formato compatibile con PolyBase e l'archiviazione dei dati in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="a0c97-258">Vengono quindi caricati i dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="a0c97-259">Impostare la proprietà `allowPolyBase` su **true**, come illustrato nell'esempio seguente per Azure Data Factory, per usare PolyBase per copiare i dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a0c97-260">Quando si imposta allowPolyBase su true, è possibile specificare proprietà specifiche di PolyBase usando il gruppo di proprietà `polyBaseSettings`.</span><span class="sxs-lookup"><span data-stu-id="a0c97-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="a0c97-261">Per informazioni dettagliate sulle proprietà che è possibile usare con polyBaseSettings, vedere la sezione [SqlDWSink](#SqlDWSink) .</span><span class="sxs-lookup"><span data-stu-id="a0c97-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="a0c97-262">Copia diretta tramite PolyBase</span><span class="sxs-lookup"><span data-stu-id="a0c97-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="a0c97-263">PolyBase di SQL Data Warehouse supporta direttamente Archiviazione BLOB di Azure e Azure Data Lake Store (mediante l'entità servizio) come origine e con requisiti di formato di file specifico.</span><span class="sxs-lookup"><span data-stu-id="a0c97-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="a0c97-264">Se i dati di origine soddisfano i criteri descritti in questa sezione, è possibile eseguire la copia direttamente dall'archivio dati di origine ad Azure SQL Data Warehouse con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="a0c97-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="a0c97-265">In caso contrario è possibile usare la [copia di staging tramite PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="a0c97-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="a0c97-266">Nell'articolo [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/) (Con Azure Data Factory è ancora più semplice e pratico individuare informazioni utili sui dati quando si usa Data Lake Store con SQL Data Warehouse) sono indicate altre informazioni utili per copiare efficacemente i dati da Data Lake Store a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="a0c97-267">Se i requisiti non vengono soddisfatti, Azure Data Factory controlla le impostazioni e usa automaticamente il meccanismo BULKINSERT per lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="a0c97-268">Il **servizio collegato all'origine** è di tipo: **AzureStorage** o **AzureDataLakeStore con autenticazione entità servizio**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="a0c97-269">Il **set di dati di input** è di tipo **AzureBlob** o **AzureDataLakeStore** e il tipo di formato nelle proprietà `type` è **OrcFormat** o **TextFormat** con le configurazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="a0c97-270">`rowDelimiter` deve essere **\n**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="a0c97-271">`nullValue` è impostato su **stringa vuota** ("") o `treatEmptyAsNull` è impostato su **true**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="a0c97-272">`encodingName` è impostato su **utf-8**, ovvero il valore **predefinito**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="a0c97-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` e `skipLineCount` non sono specificati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="a0c97-274">`compression` può essere **no compression**, **GZip** o **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="a0c97-275">Non è disponibile alcuna impostazione `skipHeaderLineCount` in **BlobSource** o **AzureDataLakeStore** per l'attività di copia nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="a0c97-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="a0c97-276">Non è disponibile alcuna impostazione `sliceIdentifierColumnName` in **SqlDWSink** per l'attività di copia nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="a0c97-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="a0c97-277">PolyBase garantisce che tutti i dati verranno aggiornati o che nessun dato verrà aggiornato in una singola esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a0c97-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="a0c97-278">Per ottenere la **ripetibilità**, è possibile usare `sqlWriterCleanupScript`.</span><span class="sxs-lookup"><span data-stu-id="a0c97-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="a0c97-279">Nell'attività di copia associata non viene usato alcun valore `columnMapping`.</span><span class="sxs-lookup"><span data-stu-id="a0c97-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="a0c97-280">copia di staging tramite PolyBase</span><span class="sxs-lookup"><span data-stu-id="a0c97-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="a0c97-281">Quando i dati di origine non soddisfano i criteri presentati nella sezione precedente, è possibile abilitare la copia dei dati tramite un'istanza di Archiviazione BLOB di Azure di gestione temporanea provvisoria (non può essere Archiviazione Premium).</span><span class="sxs-lookup"><span data-stu-id="a0c97-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="a0c97-282">In questo caso, Azure Data Factory esegue automaticamente trasformazioni sui dati in modo che soddisfino i requisiti di formato dei dati di PolyBase e quindi usa PolyBase per caricare i dati in SQL Data Warehouse e infine pulisce i dati temporanei dall'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="a0c97-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="a0c97-283">Per informazioni dettagliate sul funzionamento generale della copia dei dati tramite un BLOB di Azure di staging, vedere la sezione [Copia di staging](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="a0c97-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="a0c97-284">Quando si copiano i dati da un archivio dati locale in Azure SQL Data Warehouse usando PolyBase e la gestione temporanea, se la versione del gateway di gestione dati è precedente alla versione 2.4, il computer gateway deve disporre di JRE (Java Runtime Environment) per poter convertire i dati di origine nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="a0c97-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="a0c97-285">È consigliabile aggiornare il gateway installando la versione più recente per evitare tale dipendenza.</span><span class="sxs-lookup"><span data-stu-id="a0c97-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="a0c97-286">Per usare questa funzionalità, creare un [servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) che faccia riferimento all'account di archiviazione di Azure contenente l'archivio BLOB provvisorio e quindi specificare le proprietà `enableStaging` e `stagingSettings` per l'attività di copia come illustrato nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a0c97-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="a0c97-287">Procedure consigliate per l'uso di PolyBase</span><span class="sxs-lookup"><span data-stu-id="a0c97-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="a0c97-288">Le sezioni seguenti forniscono procedure consigliate aggiuntive a quelle descritte in [Procedure consigliate per Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="a0c97-289">Autorizzazione database obbligatoria</span><span class="sxs-lookup"><span data-stu-id="a0c97-289">Required database permission</span></span>
<span data-ttu-id="a0c97-290">Per usare PolyBase, è necessario che l'utente che è solito caricare i dati in SQL Data Warehouse disponga dell'[autorizzazione "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) nel database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a0c97-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="a0c97-291">Un modo per ottenere questo risultato consiste nell'aggiungere tale utente come membro del ruolo "db_owner".</span><span class="sxs-lookup"><span data-stu-id="a0c97-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="a0c97-292">Informazioni su come eseguire questa operazione sono disponibili nella [sezione](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization) seguente.</span><span class="sxs-lookup"><span data-stu-id="a0c97-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="a0c97-293">Limitazione alle dimensioni di righe e al tipo di dati</span><span class="sxs-lookup"><span data-stu-id="a0c97-293">Row size and data type limitation</span></span>
<span data-ttu-id="a0c97-294">Le operazioni di caricamento di PolyBase sono limitate al caricamento di righe inferiori a **1 MB** che non possono essere caricate in VARCHR(MAX), NVARCHAR(MAX) o VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="a0c97-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="a0c97-295">Vedere [qui](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="a0c97-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="a0c97-296">Se sono presenti dati di origine con righe di dimensioni superiori a 1 MB, è consigliabile suddividere verticalmente le tabelle di origine in tabelle più piccole, in cui le dimensioni massime delle righe di ogni tabella non superano il limite previsto.</span><span class="sxs-lookup"><span data-stu-id="a0c97-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="a0c97-297">Le tabelle più piccole possono essere quindi caricate usando PolyBase e unite in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="a0c97-298">Classe di risorse di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="a0c97-299">Per ottenere le migliori prestazioni possibili, considerare di assegnare una classe di risorse più ampia all'utente che carica i dati in SQL Data Warehouse tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="a0c97-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="a0c97-300">Per eseguire questa operazione, seguire la procedura descritta in [Esempio di modifica della classe di risorse di un utente](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="a0c97-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="a0c97-301">tableName in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a0c97-302">La tabella seguente fornisce esempi relativi a come specificare la proprietà **tableName** nel set di dati JSON per diverse combinazioni di nomi di schema e di tabella.</span><span class="sxs-lookup"><span data-stu-id="a0c97-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="a0c97-303">Schema di database</span><span class="sxs-lookup"><span data-stu-id="a0c97-303">DB Schema</span></span> | <span data-ttu-id="a0c97-304">Nome tabella</span><span class="sxs-lookup"><span data-stu-id="a0c97-304">Table name</span></span> | <span data-ttu-id="a0c97-305">Proprietà JSON tableName</span><span class="sxs-lookup"><span data-stu-id="a0c97-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0c97-306">dbo</span><span class="sxs-lookup"><span data-stu-id="a0c97-306">dbo</span></span> |<span data-ttu-id="a0c97-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="a0c97-307">MyTable</span></span> |<span data-ttu-id="a0c97-308">MyTable o dbo.MyTable o [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="a0c97-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="a0c97-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="a0c97-309">dbo1</span></span> |<span data-ttu-id="a0c97-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="a0c97-310">MyTable</span></span> |<span data-ttu-id="a0c97-311">dbo1.MyTable o [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="a0c97-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="a0c97-312">dbo</span><span class="sxs-lookup"><span data-stu-id="a0c97-312">dbo</span></span> |<span data-ttu-id="a0c97-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="a0c97-313">My.Table</span></span> |<span data-ttu-id="a0c97-314">[My.Table] o [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="a0c97-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="a0c97-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="a0c97-315">dbo1</span></span> |<span data-ttu-id="a0c97-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="a0c97-316">My.Table</span></span> |<span data-ttu-id="a0c97-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="a0c97-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="a0c97-318">Se viene visualizzato l'errore seguente, potrebbe essersi verificato un problema con il valore specificato per la proprietà tableName.</span><span class="sxs-lookup"><span data-stu-id="a0c97-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="a0c97-319">Per informazioni sul modo corretto di specificare i valori per la proprietà JSON tableName, vedere la relativa tabella.</span><span class="sxs-lookup"><span data-stu-id="a0c97-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="a0c97-320">Colonne con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="a0c97-320">Columns with default values</span></span>
<span data-ttu-id="a0c97-321">La funzionalità PolyBase in Data Factory accetta attualmente lo stesso numero di colonne disponibili nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a0c97-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="a0c97-322">Se si ha una tabella con quattro colonne di cui una definita con un valore predefinito, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="a0c97-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="a0c97-323">i dati di input dovranno comunque contenere quattro colonne.</span><span class="sxs-lookup"><span data-stu-id="a0c97-323">The input data should still contain four columns.</span></span> <span data-ttu-id="a0c97-324">Se si specifica un set di dati di input con 3 colonne, si verificherà un errore simile al messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="a0c97-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="a0c97-325">Il valore NULL è una forma speciale di valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="a0c97-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="a0c97-326">Se la colonna ammette valori Null, i dati di input (nel BLOB) per tale colonna possono essere vuoti, ma non possono essere mancanti dal set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="a0c97-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="a0c97-327">PolyBase inserisce NULL per tali valori in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="a0c97-328">Creazione automatica della tabella</span><span class="sxs-lookup"><span data-stu-id="a0c97-328">Auto table creation</span></span>
<span data-ttu-id="a0c97-329">Se si usa la copia guidata per copiare i dati da SQL Server o da Database SQL di Azure in SQL Data Warehouse e la tabella che corrisponde alla tabella di origine non esiste nell'archivio di destinazione, Data Factory la crea automaticamente nel data warehouse usando lo schema della tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="a0c97-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="a0c97-330">Data Factory crea la tabella nell'archivio di destinazione con lo stesso nome della tabella nell'archivio dati di origine.</span><span class="sxs-lookup"><span data-stu-id="a0c97-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="a0c97-331">I tipi di dati per le colonne vengono scelti in base al mapping dei tipi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a0c97-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="a0c97-332">Se necessario, esegue le conversioni del tipo per risolvere eventuali incompatibilità tra gli archivi di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a0c97-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="a0c97-333">Usa inoltre la distribuzione di tabella Round Robin.</span><span class="sxs-lookup"><span data-stu-id="a0c97-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="a0c97-334">Tipo di colonna di origine del Database SQL</span><span class="sxs-lookup"><span data-stu-id="a0c97-334">Source SQL Database column type</span></span> | <span data-ttu-id="a0c97-335">Tipo di colonna SQL DW di destinazione del Database (limitazione delle dimensioni)</span><span class="sxs-lookup"><span data-stu-id="a0c97-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="a0c97-336">int</span><span class="sxs-lookup"><span data-stu-id="a0c97-336">Int</span></span> | <span data-ttu-id="a0c97-337">int</span><span class="sxs-lookup"><span data-stu-id="a0c97-337">Int</span></span> |
| <span data-ttu-id="a0c97-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="a0c97-338">BigInt</span></span> | <span data-ttu-id="a0c97-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="a0c97-339">BigInt</span></span> |
| <span data-ttu-id="a0c97-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="a0c97-340">SmallInt</span></span> | <span data-ttu-id="a0c97-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="a0c97-341">SmallInt</span></span> |
| <span data-ttu-id="a0c97-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="a0c97-342">TinyInt</span></span> | <span data-ttu-id="a0c97-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="a0c97-343">TinyInt</span></span> |
| <span data-ttu-id="a0c97-344">Bit</span><span class="sxs-lookup"><span data-stu-id="a0c97-344">Bit</span></span> | <span data-ttu-id="a0c97-345">Bit</span><span class="sxs-lookup"><span data-stu-id="a0c97-345">Bit</span></span> |
| <span data-ttu-id="a0c97-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="a0c97-346">Decimal</span></span> | <span data-ttu-id="a0c97-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="a0c97-347">Decimal</span></span> |
| <span data-ttu-id="a0c97-348">Numeric</span><span class="sxs-lookup"><span data-stu-id="a0c97-348">Numeric</span></span> | <span data-ttu-id="a0c97-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="a0c97-349">Decimal</span></span> |
| <span data-ttu-id="a0c97-350">Float</span><span class="sxs-lookup"><span data-stu-id="a0c97-350">Float</span></span> | <span data-ttu-id="a0c97-351">Float</span><span class="sxs-lookup"><span data-stu-id="a0c97-351">Float</span></span> |
| <span data-ttu-id="a0c97-352">Money</span><span class="sxs-lookup"><span data-stu-id="a0c97-352">Money</span></span> | <span data-ttu-id="a0c97-353">Money</span><span class="sxs-lookup"><span data-stu-id="a0c97-353">Money</span></span> |
| <span data-ttu-id="a0c97-354">Real</span><span class="sxs-lookup"><span data-stu-id="a0c97-354">Real</span></span> | <span data-ttu-id="a0c97-355">Real</span><span class="sxs-lookup"><span data-stu-id="a0c97-355">Real</span></span> |
| <span data-ttu-id="a0c97-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="a0c97-356">SmallMoney</span></span> | <span data-ttu-id="a0c97-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="a0c97-357">SmallMoney</span></span> |
| <span data-ttu-id="a0c97-358">Binary</span><span class="sxs-lookup"><span data-stu-id="a0c97-358">Binary</span></span> | <span data-ttu-id="a0c97-359">Binary</span><span class="sxs-lookup"><span data-stu-id="a0c97-359">Binary</span></span> |
| <span data-ttu-id="a0c97-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="a0c97-360">Varbinary</span></span> | <span data-ttu-id="a0c97-361">Varbinary (fino a 8000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="a0c97-362">Data</span><span class="sxs-lookup"><span data-stu-id="a0c97-362">Date</span></span> | <span data-ttu-id="a0c97-363">Data</span><span class="sxs-lookup"><span data-stu-id="a0c97-363">Date</span></span> |
| <span data-ttu-id="a0c97-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-364">DateTime</span></span> | <span data-ttu-id="a0c97-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-365">DateTime</span></span> |
| <span data-ttu-id="a0c97-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="a0c97-366">DateTime2</span></span> | <span data-ttu-id="a0c97-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="a0c97-367">DateTime2</span></span> |
| <span data-ttu-id="a0c97-368">Time</span><span class="sxs-lookup"><span data-stu-id="a0c97-368">Time</span></span> | <span data-ttu-id="a0c97-369">Time</span><span class="sxs-lookup"><span data-stu-id="a0c97-369">Time</span></span> |
| <span data-ttu-id="a0c97-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a0c97-370">DateTimeOffset</span></span> | <span data-ttu-id="a0c97-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a0c97-371">DateTimeOffset</span></span> |
| <span data-ttu-id="a0c97-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-372">SmallDateTime</span></span> | <span data-ttu-id="a0c97-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-373">SmallDateTime</span></span> |
| <span data-ttu-id="a0c97-374">Text</span><span class="sxs-lookup"><span data-stu-id="a0c97-374">Text</span></span> | <span data-ttu-id="a0c97-375">Varchar (fino a 8000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="a0c97-376">NText</span><span class="sxs-lookup"><span data-stu-id="a0c97-376">NText</span></span> | <span data-ttu-id="a0c97-377">NVarChar (fino a 4000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="a0c97-378">Image</span><span class="sxs-lookup"><span data-stu-id="a0c97-378">Image</span></span> | <span data-ttu-id="a0c97-379">VarBinary (fino a 8000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="a0c97-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="a0c97-380">UniqueIdentifier</span></span> | <span data-ttu-id="a0c97-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="a0c97-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="a0c97-382">Char</span><span class="sxs-lookup"><span data-stu-id="a0c97-382">Char</span></span> | <span data-ttu-id="a0c97-383">Char</span><span class="sxs-lookup"><span data-stu-id="a0c97-383">Char</span></span> |
| <span data-ttu-id="a0c97-384">NChar</span><span class="sxs-lookup"><span data-stu-id="a0c97-384">NChar</span></span> | <span data-ttu-id="a0c97-385">NChar</span><span class="sxs-lookup"><span data-stu-id="a0c97-385">NChar</span></span> |
| <span data-ttu-id="a0c97-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="a0c97-386">VarChar</span></span> | <span data-ttu-id="a0c97-387">VarChar (fino a 8000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="a0c97-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="a0c97-388">NVarChar</span></span> | <span data-ttu-id="a0c97-389">NVarChar (fino a 4000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="a0c97-390">Xml</span><span class="sxs-lookup"><span data-stu-id="a0c97-390">Xml</span></span> | <span data-ttu-id="a0c97-391">Varchar (fino a 8000)</span><span class="sxs-lookup"><span data-stu-id="a0c97-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="a0c97-392">Mapping dei tipi per Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a0c97-393">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="a0c97-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="a0c97-394">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a0c97-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a0c97-395">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="a0c97-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a0c97-396">Quando si spostano dati da e verso Azure SQL Data Warehouse, vengono usati i mapping seguenti dal tipo SQL al tipo .NET e viceversa.</span><span class="sxs-lookup"><span data-stu-id="a0c97-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="a0c97-397">Il mapping è uguale al [mapping del tipo di dati di SQL Server per ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0c97-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="a0c97-398">Tipo di motore di database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="a0c97-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="a0c97-399">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a0c97-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="a0c97-400">bigint</span><span class="sxs-lookup"><span data-stu-id="a0c97-400">bigint</span></span> |<span data-ttu-id="a0c97-401">Int64</span><span class="sxs-lookup"><span data-stu-id="a0c97-401">Int64</span></span> |
| <span data-ttu-id="a0c97-402">binary</span><span class="sxs-lookup"><span data-stu-id="a0c97-402">binary</span></span> |<span data-ttu-id="a0c97-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-403">Byte[]</span></span> |
| <span data-ttu-id="a0c97-404">bit</span><span class="sxs-lookup"><span data-stu-id="a0c97-404">bit</span></span> |<span data-ttu-id="a0c97-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="a0c97-405">Boolean</span></span> |
| <span data-ttu-id="a0c97-406">char</span><span class="sxs-lookup"><span data-stu-id="a0c97-406">char</span></span> |<span data-ttu-id="a0c97-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-407">String, Char[]</span></span> |
| <span data-ttu-id="a0c97-408">date</span><span class="sxs-lookup"><span data-stu-id="a0c97-408">date</span></span> |<span data-ttu-id="a0c97-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-409">DateTime</span></span> |
| <span data-ttu-id="a0c97-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-410">Datetime</span></span> |<span data-ttu-id="a0c97-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-411">DateTime</span></span> |
| <span data-ttu-id="a0c97-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="a0c97-412">datetime2</span></span> |<span data-ttu-id="a0c97-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-413">DateTime</span></span> |
| <span data-ttu-id="a0c97-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a0c97-414">Datetimeoffset</span></span> |<span data-ttu-id="a0c97-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a0c97-415">DateTimeOffset</span></span> |
| <span data-ttu-id="a0c97-416">Decimale</span><span class="sxs-lookup"><span data-stu-id="a0c97-416">Decimal</span></span> |<span data-ttu-id="a0c97-417">Decimale</span><span class="sxs-lookup"><span data-stu-id="a0c97-417">Decimal</span></span> |
| <span data-ttu-id="a0c97-418">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="a0c97-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="a0c97-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-419">Byte[]</span></span> |
| <span data-ttu-id="a0c97-420">Float</span><span class="sxs-lookup"><span data-stu-id="a0c97-420">Float</span></span> |<span data-ttu-id="a0c97-421">Double</span><span class="sxs-lookup"><span data-stu-id="a0c97-421">Double</span></span> |
| <span data-ttu-id="a0c97-422">immagine</span><span class="sxs-lookup"><span data-stu-id="a0c97-422">image</span></span> |<span data-ttu-id="a0c97-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-423">Byte[]</span></span> |
| <span data-ttu-id="a0c97-424">int</span><span class="sxs-lookup"><span data-stu-id="a0c97-424">int</span></span> |<span data-ttu-id="a0c97-425">Int32</span><span class="sxs-lookup"><span data-stu-id="a0c97-425">Int32</span></span> |
| <span data-ttu-id="a0c97-426">money</span><span class="sxs-lookup"><span data-stu-id="a0c97-426">money</span></span> |<span data-ttu-id="a0c97-427">Decimale</span><span class="sxs-lookup"><span data-stu-id="a0c97-427">Decimal</span></span> |
| <span data-ttu-id="a0c97-428">nchar</span><span class="sxs-lookup"><span data-stu-id="a0c97-428">nchar</span></span> |<span data-ttu-id="a0c97-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-429">String, Char[]</span></span> |
| <span data-ttu-id="a0c97-430">ntext</span><span class="sxs-lookup"><span data-stu-id="a0c97-430">ntext</span></span> |<span data-ttu-id="a0c97-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-431">String, Char[]</span></span> |
| <span data-ttu-id="a0c97-432">numeric</span><span class="sxs-lookup"><span data-stu-id="a0c97-432">numeric</span></span> |<span data-ttu-id="a0c97-433">Decimale</span><span class="sxs-lookup"><span data-stu-id="a0c97-433">Decimal</span></span> |
| <span data-ttu-id="a0c97-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="a0c97-434">nvarchar</span></span> |<span data-ttu-id="a0c97-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-435">String, Char[]</span></span> |
| <span data-ttu-id="a0c97-436">real</span><span class="sxs-lookup"><span data-stu-id="a0c97-436">real</span></span> |<span data-ttu-id="a0c97-437">Single</span><span class="sxs-lookup"><span data-stu-id="a0c97-437">Single</span></span> |
| <span data-ttu-id="a0c97-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="a0c97-438">rowversion</span></span> |<span data-ttu-id="a0c97-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-439">Byte[]</span></span> |
| <span data-ttu-id="a0c97-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="a0c97-440">smalldatetime</span></span> |<span data-ttu-id="a0c97-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0c97-441">DateTime</span></span> |
| <span data-ttu-id="a0c97-442">smallint</span><span class="sxs-lookup"><span data-stu-id="a0c97-442">smallint</span></span> |<span data-ttu-id="a0c97-443">Int16</span><span class="sxs-lookup"><span data-stu-id="a0c97-443">Int16</span></span> |
| <span data-ttu-id="a0c97-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="a0c97-444">smallmoney</span></span> |<span data-ttu-id="a0c97-445">Decimale</span><span class="sxs-lookup"><span data-stu-id="a0c97-445">Decimal</span></span> |
| <span data-ttu-id="a0c97-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="a0c97-446">sql_variant</span></span> |<span data-ttu-id="a0c97-447">Object *</span><span class="sxs-lookup"><span data-stu-id="a0c97-447">Object *</span></span> |
| <span data-ttu-id="a0c97-448">text</span><span class="sxs-lookup"><span data-stu-id="a0c97-448">text</span></span> |<span data-ttu-id="a0c97-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-449">String, Char[]</span></span> |
| <span data-ttu-id="a0c97-450">time</span><span class="sxs-lookup"><span data-stu-id="a0c97-450">time</span></span> |<span data-ttu-id="a0c97-451">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="a0c97-451">TimeSpan</span></span> |
| <span data-ttu-id="a0c97-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="a0c97-452">timestamp</span></span> |<span data-ttu-id="a0c97-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-453">Byte[]</span></span> |
| <span data-ttu-id="a0c97-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="a0c97-454">tinyint</span></span> |<span data-ttu-id="a0c97-455">Byte</span><span class="sxs-lookup"><span data-stu-id="a0c97-455">Byte</span></span> |
| <span data-ttu-id="a0c97-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="a0c97-456">uniqueidentifier</span></span> |<span data-ttu-id="a0c97-457">Guid</span><span class="sxs-lookup"><span data-stu-id="a0c97-457">Guid</span></span> |
| <span data-ttu-id="a0c97-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="a0c97-458">varbinary</span></span> |<span data-ttu-id="a0c97-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-459">Byte[]</span></span> |
| <span data-ttu-id="a0c97-460">varchar</span><span class="sxs-lookup"><span data-stu-id="a0c97-460">varchar</span></span> |<span data-ttu-id="a0c97-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="a0c97-461">String, Char[]</span></span> |
| <span data-ttu-id="a0c97-462">xml</span><span class="sxs-lookup"><span data-stu-id="a0c97-462">xml</span></span> |<span data-ttu-id="a0c97-463">xml</span><span class="sxs-lookup"><span data-stu-id="a0c97-463">Xml</span></span> |

<span data-ttu-id="a0c97-464">È anche possibile eseguire il mapping delle colonne del set di dati di origine alle colonne del set di dati sink nella definizione dell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a0c97-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="a0c97-465">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="a0c97-466">Esempi JSON per la copia dei dati da e verso SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="a0c97-467">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a0c97-468">Tali esempi mostrano come copiare dati in e da Azure SQL Data Warehouse e in e dall'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="a0c97-469">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c97-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="a0c97-470">Esempio: Copiare i dati da Azure SQL Data Warehouse al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="a0c97-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="a0c97-471">L'esempio definisce le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="a0c97-472">Un servizio collegato di tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="a0c97-473">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a0c97-474">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a0c97-475">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a0c97-476">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlDWSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a0c97-477">L'esempio copia ogni ora i dati di una serie temporale (con frequenza oraria, giornaliera e così via) da una tabella del database di Azure SQL Data Warehouse a un BLOB.</span><span class="sxs-lookup"><span data-stu-id="a0c97-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="a0c97-478">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="a0c97-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a0c97-479">**Servizio collegato di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="a0c97-480">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="a0c97-481">**Set di dati di input di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="a0c97-482">L'esempio presuppone che sia stata creata una tabella "MyTable" in Azure SQL Data Warehouse e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="a0c97-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="a0c97-483">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="a0c97-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="a0c97-484">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a0c97-485">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="a0c97-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a0c97-486">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a0c97-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a0c97-487">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="a0c97-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a0c97-488">**Attività di copia in una pipeline con SqlDWSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="a0c97-489">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a0c97-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a0c97-490">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **SqlDWSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a0c97-491">La query SQL specificata per la proprietà **SqlReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="a0c97-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="a0c97-492">Nell'esempio, la proprietà **sqlReaderQuery** è specificata per SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="a0c97-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="a0c97-493">L'attività di copia esegue questa query nell'origine dell’SQL Data Warehouse di Azure per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="a0c97-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="a0c97-494">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="a0c97-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="a0c97-495">Se non si specifica il parametro sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura del set di dati JSON vengono usate per compilare una query (selezionare column1, column2 da mytable) da eseguire nell’SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a0c97-496">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="a0c97-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="a0c97-497">Esempio: Copiare i dati dal BLOB di Azure ad Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0c97-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a0c97-498">L'esempio definisce le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c97-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="a0c97-499">Un servizio collegato di tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="a0c97-500">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a0c97-501">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="a0c97-502">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="a0c97-503">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a0c97-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="a0c97-504">L'esempio copia ogni ora i dati di una serie temporale (con frequenza oraria, giornaliera e così via) da un BLOB di Azure a una tabella del database di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="a0c97-505">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="a0c97-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a0c97-506">**Servizio collegato di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="a0c97-507">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="a0c97-508">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="a0c97-509">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="a0c97-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a0c97-510">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a0c97-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a0c97-511">Il percorso della cartella usa le parti di anno, mese e giorno della data/ora di inizio e il nome file usa la parte relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="a0c97-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="a0c97-512">L'impostazione di "external" su "true" comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="a0c97-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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
<span data-ttu-id="a0c97-513">**Set di dati di output di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="a0c97-514">Nell’esempio vengono copiati dati in una tabella denominata "MyTable" in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a0c97-515">Creare la tabella in Azure SQL Data Warehouse con lo stesso numero di colonne previsto nel file CSV del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a0c97-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="a0c97-516">Alla tabella vengono aggiunte nuove righe ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a0c97-516">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="a0c97-517">**Copiare attività in una pipeline con BlobSource e SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="a0c97-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="a0c97-518">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a0c97-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a0c97-519">Nella definizione JSON della pipeline il tipo di **origine** è impostato su **BlobSource** e il tipo di **sink** è impostato su **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="a0c97-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="a0c97-520">Per una procedura dettagliata, vedere gli articoli [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md) e [Caricare i dati con Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) nella documentazione di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0c97-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a0c97-521">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a0c97-521">Performance and Tuning</span></span>
<span data-ttu-id="a0c97-522">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a0c97-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
