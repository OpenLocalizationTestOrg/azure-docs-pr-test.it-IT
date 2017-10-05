---
title: Copiare dati nel/dal database SQL di Azure | Microsoft Docs
description: Informazioni su come copiare dati da e verso il database SQL di Azure mediante Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="efba7-103">Copiare dati da e nel database SQL di Azure con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="efba7-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="efba7-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="efba7-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="efba7-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="efba7-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="efba7-106">Supported scenarios</span></span>
<span data-ttu-id="efba7-107">È possibile copiare i dati **da un database SQL di Azure** negli archivi di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="efba7-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="efba7-108">È possibile copiare i dati dagli archivi dati seguenti **a un database SQL di Azure**:</span><span class="sxs-lookup"><span data-stu-id="efba7-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="efba7-109">Tipo di autenticazione supportato</span><span class="sxs-lookup"><span data-stu-id="efba7-109">Supported authentication type</span></span>
<span data-ttu-id="efba7-110">Il connettore per database SQL di Azure supporta l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="efba7-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="efba7-111">Introduzione</span><span class="sxs-lookup"><span data-stu-id="efba7-111">Getting started</span></span>
<span data-ttu-id="efba7-112">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un database SQL di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="efba7-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="efba7-113">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="efba7-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="efba7-114">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="efba7-115">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="efba7-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="efba7-116">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="efba7-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="efba7-117">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="efba7-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="efba7-118">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="efba7-118">Create a **data factory**.</span></span> <span data-ttu-id="efba7-119">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="efba7-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="efba7-120">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="efba7-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="efba7-121">Ad esempio, se si copiano i dati da un'archiviazione BLOB di Azure in un database SQL di Azure, si creano due servizi collegati per collegare l'account di archiviazione di Azure e il database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="efba7-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="efba7-122">Per le proprietà del servizio collegato specifiche per il database SQL di Azure, vedere la sezione sulle [proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="efba7-123">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="efba7-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="efba7-124">Nell'esempio citato nel passaggio precedente, si crea un set di dati per specificare un contenitore BLOB e la cartella che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="efba7-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="efba7-125">Si crea anche un altro set di dati per specificare la tabella SQL nel database SQL di Azure che contiene i dati copiati dall'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="efba7-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="efba7-126">Per le proprietà del set di dati specifiche per Azure Data Lake Store, vedere la sezione sulle [proprietà del set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="efba7-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="efba7-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="efba7-128">Nell'esempio indicato in precedenza si usa BlobSource come origine e SqlSink come sink per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="efba7-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="efba7-129">Analogamente, se si esegue la copia dal database SQL di Azure nell'archiviazione BLOB di Azure, si usa SqlSource e BlobSink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="efba7-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="efba7-130">Per le proprietà dell'attività di copia specifiche per il database SQL di Azure, vedere la sezione sulle [proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="efba7-131">Per informazioni dettagliate su come usare un archivio dati come origine o come sink, fare clic sul collegamento nella sezione precedente per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="efba7-132">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="efba7-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="efba7-133">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="efba7-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="efba7-134">Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso un database SQL di Azure, vedere la sezione degli [esempi JSON](#json-examples-for-copying-data-to-and-from-sql-database) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="efba7-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="efba7-135">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="efba7-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="efba7-136">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="efba7-136">Linked service properties</span></span>
<span data-ttu-id="efba7-137">Un servizio collegato SQL di Azure collega un database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="efba7-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="efba7-138">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="efba7-139">Proprietà</span><span class="sxs-lookup"><span data-stu-id="efba7-139">Property</span></span> | <span data-ttu-id="efba7-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="efba7-140">Description</span></span> | <span data-ttu-id="efba7-141">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="efba7-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efba7-142">type</span><span class="sxs-lookup"><span data-stu-id="efba7-142">type</span></span> |<span data-ttu-id="efba7-143">La proprietà del tipo deve essere impostata su: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="efba7-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="efba7-144">Sì</span><span class="sxs-lookup"><span data-stu-id="efba7-144">Yes</span></span> |
| <span data-ttu-id="efba7-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="efba7-145">connectionString</span></span> |<span data-ttu-id="efba7-146">Specificare le informazioni necessarie per connettersi all'istanza di database SQL di Azure per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="efba7-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="efba7-147">È supportata solo l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="efba7-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="efba7-148">Sì</span><span class="sxs-lookup"><span data-stu-id="efba7-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="efba7-149">Configurare il [firewall del database SQL di Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e il server di database in modo da [consentire ai servizi di Azure di accedere al server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="efba7-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="efba7-150">Se si copiano dati nel database SQL di Azure dall'esterno di Azure e da origini dati locali con gateway di data factory, configurare anche un intervallo di indirizzi IP appropriato per il computer che invia dati al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="efba7-151">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="efba7-151">Dataset properties</span></span>
<span data-ttu-id="efba7-152">Per specificare un set di dati per rappresentare i dati di input o outpui in un database SQL di Azure, impostare la proprietà del tipo del set di dati su **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="efba7-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="efba7-153">Impostare la proprietà **linkedServiceName** del set di dati sul nome del servizio collegato SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="efba7-154">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="efba7-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="efba7-155">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="efba7-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="efba7-156">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="efba7-157">La sezione **typeProperties** per il set di dati di tipo **AzureSqlTable** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="efba7-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="efba7-158">Proprietà</span><span class="sxs-lookup"><span data-stu-id="efba7-158">Property</span></span> | <span data-ttu-id="efba7-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="efba7-159">Description</span></span> | <span data-ttu-id="efba7-160">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="efba7-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efba7-161">tableName</span><span class="sxs-lookup"><span data-stu-id="efba7-161">tableName</span></span> |<span data-ttu-id="efba7-162">Nome della tabella o vista nell'istanza di database SQL di Azure a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="efba7-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="efba7-163">Sì</span><span class="sxs-lookup"><span data-stu-id="efba7-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="efba7-164">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="efba7-164">Copy activity properties</span></span>
<span data-ttu-id="efba7-165">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="efba7-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="efba7-166">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="efba7-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="efba7-167">L'attività di copia accetta solo un input e produce solo un output.</span><span class="sxs-lookup"><span data-stu-id="efba7-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="efba7-168">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="efba7-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="efba7-169">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="efba7-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="efba7-170">Se si effettua il trasferimento dei dati da un database SQL di Azure, impostare il tipo di origine nell'attività di copia su **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="efba7-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="efba7-171">Analogamente, se si effettua il trasferimento dei dati in un database SQL di Azure, impostare il tipo di sink nell'attività di copia su **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="efba7-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="efba7-172">Questa sezione presenta un elenco delle proprietà supportate da SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="efba7-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="efba7-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="efba7-173">SqlSource</span></span>
<span data-ttu-id="efba7-174">In caso di attività di copia con origine di tipo **SqlSource**, nella sezione **typeProperties** sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="efba7-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="efba7-175">Proprietà</span><span class="sxs-lookup"><span data-stu-id="efba7-175">Property</span></span> | <span data-ttu-id="efba7-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="efba7-176">Description</span></span> | <span data-ttu-id="efba7-177">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="efba7-177">Allowed values</span></span> | <span data-ttu-id="efba7-178">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="efba7-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="efba7-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="efba7-179">sqlReaderQuery</span></span> |<span data-ttu-id="efba7-180">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-180">Use the custom query to read data.</span></span> |<span data-ttu-id="efba7-181">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="efba7-181">SQL query string.</span></span> <span data-ttu-id="efba7-182">Esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="efba7-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="efba7-183">No</span><span class="sxs-lookup"><span data-stu-id="efba7-183">No</span></span> |
| <span data-ttu-id="efba7-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="efba7-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="efba7-185">Nome della stored procedure che legge i dati dalla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="efba7-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="efba7-186">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-186">Name of the stored procedure.</span></span> <span data-ttu-id="efba7-187">L'ultima istruzione SQL deve essere un'istruzione SELECT nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="efba7-188">No</span><span class="sxs-lookup"><span data-stu-id="efba7-188">No</span></span> |
| <span data-ttu-id="efba7-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="efba7-189">storedProcedureParameters</span></span> |<span data-ttu-id="efba7-190">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="efba7-191">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="efba7-191">Name/value pairs.</span></span> <span data-ttu-id="efba7-192">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="efba7-193">No</span><span class="sxs-lookup"><span data-stu-id="efba7-193">No</span></span> |

<span data-ttu-id="efba7-194">Se la proprietà **sqlReaderQuery** è specificata per SqlSource, l'attività di copia esegue questa query nell'origine del database SQL di Azure per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="efba7-195">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="efba7-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="efba7-196">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura del set di dati JSON vengono usate per compilare una query (`select column1, column2 from mytable`) da eseguire sul database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="efba7-197">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="efba7-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="efba7-198">Quando si usa **sqlReaderStoredProcedureName** è necessario specificare un valore per la proprietà **tableName** nel set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="efba7-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="efba7-199">Non sono disponibili convalide eseguite su questa tabella.</span><span class="sxs-lookup"><span data-stu-id="efba7-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="efba7-200">Esempio SqlSource</span><span class="sxs-lookup"><span data-stu-id="efba7-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="efba7-201">**Definizione della stored procedure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="efba7-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="efba7-202">SqlSink</span></span>
<span data-ttu-id="efba7-203">**SqlSink** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="efba7-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="efba7-204">Proprietà</span><span class="sxs-lookup"><span data-stu-id="efba7-204">Property</span></span> | <span data-ttu-id="efba7-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="efba7-205">Description</span></span> | <span data-ttu-id="efba7-206">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="efba7-206">Allowed values</span></span> | <span data-ttu-id="efba7-207">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="efba7-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="efba7-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="efba7-208">writeBatchTimeout</span></span> |<span data-ttu-id="efba7-209">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="efba7-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="efba7-210">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="efba7-210">timespan</span></span><br/><br/> <span data-ttu-id="efba7-211">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="efba7-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="efba7-212">No</span><span class="sxs-lookup"><span data-stu-id="efba7-212">No</span></span> |
| <span data-ttu-id="efba7-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="efba7-213">writeBatchSize</span></span> |<span data-ttu-id="efba7-214">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="efba7-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="efba7-215">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="efba7-215">Integer (number of rows)</span></span> |<span data-ttu-id="efba7-216">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="efba7-216">No (default: 10000)</span></span> |
| <span data-ttu-id="efba7-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="efba7-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="efba7-218">Specificare una query da eseguire nell'attività di copia per pulire i dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="efba7-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="efba7-219">Per altre informazioni, vedere la [copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="efba7-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="efba7-220">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="efba7-220">A query statement.</span></span> |<span data-ttu-id="efba7-221">No</span><span class="sxs-lookup"><span data-stu-id="efba7-221">No</span></span> |
| <span data-ttu-id="efba7-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="efba7-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="efba7-223">Specificare il nome di una colonna in cui inserire nell'attività di copia l'identificatore di sezione generato automaticamente che verrà usato per pulire i dati di una sezione specifica quando viene ripetuta l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="efba7-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="efba7-224">Per altre informazioni, vedere la [copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="efba7-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="efba7-225">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="efba7-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="efba7-226">No</span><span class="sxs-lookup"><span data-stu-id="efba7-226">No</span></span> |
| <span data-ttu-id="efba7-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="efba7-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="efba7-228">Nome della stored procedure che esegue l'upsert (aggiornamenti/inserimenti) nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="efba7-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="efba7-229">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-229">Name of the stored procedure.</span></span> |<span data-ttu-id="efba7-230">No</span><span class="sxs-lookup"><span data-stu-id="efba7-230">No</span></span> |
| <span data-ttu-id="efba7-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="efba7-231">storedProcedureParameters</span></span> |<span data-ttu-id="efba7-232">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="efba7-233">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="efba7-233">Name/value pairs.</span></span> <span data-ttu-id="efba7-234">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="efba7-235">No</span><span class="sxs-lookup"><span data-stu-id="efba7-235">No</span></span> |
| <span data-ttu-id="efba7-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="efba7-236">sqlWriterTableType</span></span> |<span data-ttu-id="efba7-237">Specificare il nome di un tipo di tabella da usare nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="efba7-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="efba7-238">L'attività di copia rende i dati spostati disponibili in una tabella temporanea con questo tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="efba7-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="efba7-239">Il codice della stored procedure può quindi unire i dati copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="efba7-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="efba7-240">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="efba7-240">A table type name.</span></span> |<span data-ttu-id="efba7-241">No</span><span class="sxs-lookup"><span data-stu-id="efba7-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="efba7-242">Esempio SqlSink</span><span class="sxs-lookup"><span data-stu-id="efba7-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="efba7-243">Esempi JSON per la copia dei dati da e verso un database SQL</span><span class="sxs-lookup"><span data-stu-id="efba7-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="efba7-244">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="efba7-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="efba7-245">Tali esempi mostrano come copiare dati in e da un database SQL di Azure e un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="efba7-246">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="efba7-247">Esempio: Copiare i dati dal database SQL di Azure SQL nel BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="efba7-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="efba7-248">L'esempio definisce le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="efba7-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="efba7-249">Un servizio collegato di tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="efba7-250">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="efba7-251">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="efba7-252">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="efba7-253">Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="efba7-254">L'esempio copia ogni ora i dati di una serie temporale (con frequenza oraria, giornaliera e così via) da una tabella del database SQL di Azure a un BLOB.</span><span class="sxs-lookup"><span data-stu-id="efba7-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="efba7-255">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="efba7-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="efba7-256">**Servizio collegato per il database SQL Azure.**</span><span class="sxs-lookup"><span data-stu-id="efba7-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="efba7-257">Vedere la sezione sul [servizio collegato SQL di Azure](#linked-service) per l'elenco delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="efba7-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="efba7-258">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="efba7-259">Vedere l'articolo [BLOB di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per l'elenco delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="efba7-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="efba7-260">**Set di dati di input SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="efba7-261">L'esempio presuppone che sia stata creata una tabella "MyTable" in SQL Azure e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="efba7-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="efba7-262">L'impostazione di "external" su "true" comunica al servizio Azure Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="efba7-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="efba7-263">Vedere la sezione sulle [proprietà del tipo di set di dati SQL di Azure](#dataset) per l'elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="efba7-264">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="efba7-265">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="efba7-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="efba7-266">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="efba7-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="efba7-267">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="efba7-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="efba7-268">Vedere la sezione sulle [proprietà del tipo di set di dati BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties) per l'elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="efba7-269">**Un'attività di copia in una pipeline con un'origine SQL e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="efba7-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="efba7-270">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="efba7-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="efba7-271">Nella definizione JSON della pipeline, il tipo **source** è impostato su **SqlSource** e il tipo **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="efba7-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="efba7-272">La query SQL specificata per la proprietà **SqlReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="efba7-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="efba7-273">Nell'esempio, la proprietà **sqlReaderQuery** è specificata per SqlSource.</span><span class="sxs-lookup"><span data-stu-id="efba7-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="efba7-274">L'attività di copia esegue questa query nell'origine del database SQL di Azure per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="efba7-275">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="efba7-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="efba7-276">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura del set di dati JSON vengono usate per compilare una query da eseguire sul database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="efba7-277">Ad esempio: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="efba7-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="efba7-278">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="efba7-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="efba7-279">Vedere la sezione [SqlSource](#sqlsource) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) per l'elenco delle proprietà supportate da SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="efba7-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="efba7-280">Esempio: Copiare i dati dal BLOB di Azure nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="efba7-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="efba7-281">L'esempio definisce le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="efba7-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="efba7-282">Un servizio collegato di tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="efba7-283">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="efba7-284">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="efba7-285">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="efba7-286">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="efba7-287">L'esempio copia ogni ora i dati di una serie temporale (con frequenza oraria, giornaliera e così via) da un BLOB di Azure a una tabella del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="efba7-288">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="efba7-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="efba7-289">**Servizio collegato SQL di Azure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="efba7-290">Vedere la sezione sul [servizio collegato SQL di Azure](#linked-service) per l'elenco delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="efba7-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="efba7-291">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="efba7-292">Vedere l'articolo [BLOB di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per l'elenco delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="efba7-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="efba7-293">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="efba7-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="efba7-294">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="efba7-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="efba7-295">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="efba7-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="efba7-296">Il percorso della cartella usa le parti di anno, mese e giorno della data/ora di inizio e il nome file usa la parte relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="efba7-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="efba7-297">L'impostazione di "external" su "true" comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="efba7-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="efba7-298">Vedere la sezione sulle [proprietà del tipo di set di dati BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties) per l'elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="efba7-299">**Set di dati di aoutput del database SQL di Azure**</span><span class="sxs-lookup"><span data-stu-id="efba7-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="efba7-300">L'esempio copia dati in una tabella denominata "MyTable" in SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="efba7-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="efba7-301">Creare la tabella nel database SQL di Azure con lo stesso numero di colonne previsto nel file CSV del BLOB.</span><span class="sxs-lookup"><span data-stu-id="efba7-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="efba7-302">Alla tabella vengono aggiunte nuove righe ogni ora.</span><span class="sxs-lookup"><span data-stu-id="efba7-302">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="efba7-303">Vedere la sezione sulle [proprietà del tipo di set di dati SQL di Azure](#dataset) per l'elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="efba7-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="efba7-304">**Un'attività di copia in una pipeline con un'origine BLOB e un sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="efba7-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="efba7-305">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="efba7-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="efba7-306">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **BlobSource** e il tipo **sink** è impostato su **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="efba7-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="efba7-307">Per l'elenco delle proprietà supportate da SqlSink e BlobSink, vedere la sezione [SqlSink](#sqlsink) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efba7-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="efba7-308">Colonne Identity nel database di destinazione</span><span class="sxs-lookup"><span data-stu-id="efba7-308">Identity columns in the target database</span></span>
<span data-ttu-id="efba7-309">In questa sezione viene fornito un esempio per la copia di dati da una tabella di origine senza una colonna identity in una tabella di destinazione con una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="efba7-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="efba7-310">**Tabella di origine:**</span><span class="sxs-lookup"><span data-stu-id="efba7-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="efba7-311">**Tabella di destinazione:**</span><span class="sxs-lookup"><span data-stu-id="efba7-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="efba7-312">Si noti che la tabella di destinazione contiene una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="efba7-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="efba7-313">**Definizione JSON del set di dati di origine**</span><span class="sxs-lookup"><span data-stu-id="efba7-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="efba7-314">**Definizione JSON del set di dati di destinazione**</span><span class="sxs-lookup"><span data-stu-id="efba7-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="efba7-315">Si noti che la tabella di origine e la tabella di destinazione hanno schemi diversi (la destinazione include una colonna aggiuntiva identity).</span><span class="sxs-lookup"><span data-stu-id="efba7-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="efba7-316">In questo scenario è necessario specificare la proprietà **structure** nella definizione del set di dati di destinazione che non include la colonna identity.</span><span class="sxs-lookup"><span data-stu-id="efba7-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="efba7-317">Chiamare una stored procedure da un sink SQL</span><span class="sxs-lookup"><span data-stu-id="efba7-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="efba7-318">Per un esempio di come chiamare una stored procedure da un sink SQL in un'attività di copia di una pipeline, vedere l'articolo su come [richiamare una stored procedure per il sink SQL nell'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="efba7-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="efba7-319">Mapping dei tipi per il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="efba7-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="efba7-320">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="efba7-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="efba7-321">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="efba7-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="efba7-322">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="efba7-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="efba7-323">Quando si spostano dati da e verso il database SQL di Azure vengono usati i mapping seguenti dal tipo SQL al tipo .NET e viceversa.</span><span class="sxs-lookup"><span data-stu-id="efba7-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="efba7-324">Il mapping è uguale al mapping del tipo di dati di SQL Server per ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="efba7-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="efba7-325">Tipo di motore di database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="efba7-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="efba7-326">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="efba7-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="efba7-327">bigint</span><span class="sxs-lookup"><span data-stu-id="efba7-327">bigint</span></span> |<span data-ttu-id="efba7-328">Int64</span><span class="sxs-lookup"><span data-stu-id="efba7-328">Int64</span></span> |
| <span data-ttu-id="efba7-329">binary</span><span class="sxs-lookup"><span data-stu-id="efba7-329">binary</span></span> |<span data-ttu-id="efba7-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efba7-330">Byte[]</span></span> |
| <span data-ttu-id="efba7-331">bit</span><span class="sxs-lookup"><span data-stu-id="efba7-331">bit</span></span> |<span data-ttu-id="efba7-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="efba7-332">Boolean</span></span> |
| <span data-ttu-id="efba7-333">char</span><span class="sxs-lookup"><span data-stu-id="efba7-333">char</span></span> |<span data-ttu-id="efba7-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="efba7-334">String, Char[]</span></span> |
| <span data-ttu-id="efba7-335">date</span><span class="sxs-lookup"><span data-stu-id="efba7-335">date</span></span> |<span data-ttu-id="efba7-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="efba7-336">DateTime</span></span> |
| <span data-ttu-id="efba7-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="efba7-337">Datetime</span></span> |<span data-ttu-id="efba7-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="efba7-338">DateTime</span></span> |
| <span data-ttu-id="efba7-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="efba7-339">datetime2</span></span> |<span data-ttu-id="efba7-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="efba7-340">DateTime</span></span> |
| <span data-ttu-id="efba7-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="efba7-341">Datetimeoffset</span></span> |<span data-ttu-id="efba7-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="efba7-342">DateTimeOffset</span></span> |
| <span data-ttu-id="efba7-343">Decimale</span><span class="sxs-lookup"><span data-stu-id="efba7-343">Decimal</span></span> |<span data-ttu-id="efba7-344">Decimale</span><span class="sxs-lookup"><span data-stu-id="efba7-344">Decimal</span></span> |
| <span data-ttu-id="efba7-345">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="efba7-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="efba7-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efba7-346">Byte[]</span></span> |
| <span data-ttu-id="efba7-347">Float</span><span class="sxs-lookup"><span data-stu-id="efba7-347">Float</span></span> |<span data-ttu-id="efba7-348">Double</span><span class="sxs-lookup"><span data-stu-id="efba7-348">Double</span></span> |
| <span data-ttu-id="efba7-349">immagine</span><span class="sxs-lookup"><span data-stu-id="efba7-349">image</span></span> |<span data-ttu-id="efba7-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efba7-350">Byte[]</span></span> |
| <span data-ttu-id="efba7-351">int</span><span class="sxs-lookup"><span data-stu-id="efba7-351">int</span></span> |<span data-ttu-id="efba7-352">Int32</span><span class="sxs-lookup"><span data-stu-id="efba7-352">Int32</span></span> |
| <span data-ttu-id="efba7-353">money</span><span class="sxs-lookup"><span data-stu-id="efba7-353">money</span></span> |<span data-ttu-id="efba7-354">Decimale</span><span class="sxs-lookup"><span data-stu-id="efba7-354">Decimal</span></span> |
| <span data-ttu-id="efba7-355">nchar</span><span class="sxs-lookup"><span data-stu-id="efba7-355">nchar</span></span> |<span data-ttu-id="efba7-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="efba7-356">String, Char[]</span></span> |
| <span data-ttu-id="efba7-357">ntext</span><span class="sxs-lookup"><span data-stu-id="efba7-357">ntext</span></span> |<span data-ttu-id="efba7-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="efba7-358">String, Char[]</span></span> |
| <span data-ttu-id="efba7-359">numeric</span><span class="sxs-lookup"><span data-stu-id="efba7-359">numeric</span></span> |<span data-ttu-id="efba7-360">Decimale</span><span class="sxs-lookup"><span data-stu-id="efba7-360">Decimal</span></span> |
| <span data-ttu-id="efba7-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="efba7-361">nvarchar</span></span> |<span data-ttu-id="efba7-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="efba7-362">String, Char[]</span></span> |
| <span data-ttu-id="efba7-363">real</span><span class="sxs-lookup"><span data-stu-id="efba7-363">real</span></span> |<span data-ttu-id="efba7-364">Single</span><span class="sxs-lookup"><span data-stu-id="efba7-364">Single</span></span> |
| <span data-ttu-id="efba7-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="efba7-365">rowversion</span></span> |<span data-ttu-id="efba7-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efba7-366">Byte[]</span></span> |
| <span data-ttu-id="efba7-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="efba7-367">smalldatetime</span></span> |<span data-ttu-id="efba7-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="efba7-368">DateTime</span></span> |
| <span data-ttu-id="efba7-369">smallint</span><span class="sxs-lookup"><span data-stu-id="efba7-369">smallint</span></span> |<span data-ttu-id="efba7-370">Int16</span><span class="sxs-lookup"><span data-stu-id="efba7-370">Int16</span></span> |
| <span data-ttu-id="efba7-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="efba7-371">smallmoney</span></span> |<span data-ttu-id="efba7-372">Decimale</span><span class="sxs-lookup"><span data-stu-id="efba7-372">Decimal</span></span> |
| <span data-ttu-id="efba7-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="efba7-373">sql_variant</span></span> |<span data-ttu-id="efba7-374">Object *</span><span class="sxs-lookup"><span data-stu-id="efba7-374">Object *</span></span> |
| <span data-ttu-id="efba7-375">text</span><span class="sxs-lookup"><span data-stu-id="efba7-375">text</span></span> |<span data-ttu-id="efba7-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="efba7-376">String, Char[]</span></span> |
| <span data-ttu-id="efba7-377">time</span><span class="sxs-lookup"><span data-stu-id="efba7-377">time</span></span> |<span data-ttu-id="efba7-378">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="efba7-378">TimeSpan</span></span> |
| <span data-ttu-id="efba7-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="efba7-379">timestamp</span></span> |<span data-ttu-id="efba7-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efba7-380">Byte[]</span></span> |
| <span data-ttu-id="efba7-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="efba7-381">tinyint</span></span> |<span data-ttu-id="efba7-382">Byte</span><span class="sxs-lookup"><span data-stu-id="efba7-382">Byte</span></span> |
| <span data-ttu-id="efba7-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="efba7-383">uniqueidentifier</span></span> |<span data-ttu-id="efba7-384">Guid</span><span class="sxs-lookup"><span data-stu-id="efba7-384">Guid</span></span> |
| <span data-ttu-id="efba7-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="efba7-385">varbinary</span></span> |<span data-ttu-id="efba7-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efba7-386">Byte[]</span></span> |
| <span data-ttu-id="efba7-387">varchar</span><span class="sxs-lookup"><span data-stu-id="efba7-387">varchar</span></span> |<span data-ttu-id="efba7-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="efba7-388">String, Char[]</span></span> |
| <span data-ttu-id="efba7-389">xml</span><span class="sxs-lookup"><span data-stu-id="efba7-389">xml</span></span> |<span data-ttu-id="efba7-390">xml</span><span class="sxs-lookup"><span data-stu-id="efba7-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="efba7-391">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="efba7-391">Map source to sink columns</span></span>
<span data-ttu-id="efba7-392">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="efba7-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="efba7-393">Copia ripetibile</span><span class="sxs-lookup"><span data-stu-id="efba7-393">Repeatable copy</span></span>
<span data-ttu-id="efba7-394">Quando si copiano dati in un database SQL Server, per impostazione predefinita l'attività di copia accoda i dati alla tabella di sink.</span><span class="sxs-lookup"><span data-stu-id="efba7-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="efba7-395">Per eseguire invece un UPSERT, vedere l'articolo [Scrittura ripetibile in SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="efba7-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="efba7-396">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="efba7-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="efba7-397">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="efba7-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="efba7-398">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="efba7-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="efba7-399">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="efba7-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="efba7-400">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="efba7-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="efba7-401">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="efba7-401">Performance and Tuning</span></span>
<span data-ttu-id="efba7-402">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="efba7-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
