---
title: aaaCopy dati da e verso Azure SQL Data Warehouse | Documenti Microsoft
description: Informazioni su come toocopy dati da e verso Azure SQL Data Warehouse utilizzando Data Factory di Azure
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
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="d95b6-103">Copia dati tooand da usando Azure Data Factory di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="d95b6-104">Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove a/da Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d95b6-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="d95b6-106">tooachieve prestazioni ottimali, utilizzare i dati di PolyBase tooload in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d95b6-107">Hello [dati tooload usare PolyBase in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sezione include dettagli.</span><span class="sxs-lookup"><span data-stu-id="d95b6-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="d95b6-108">Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="d95b6-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d95b6-109">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="d95b6-109">Supported scenarios</span></span>
<span data-ttu-id="d95b6-110">È possibile copiare dati **da Azure SQL Data Warehouse** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="d95b6-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d95b6-111">È possibile copiare dati da archivi dati seguenti hello **tooAzure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="d95b6-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="d95b6-112">Quando si copiano dati da tooAzure di SQL Server o Database SQL di Azure SQL Data Warehouse, se non esiste alcuna tabella hello nell'archivio di destinazione hello, Data Factory potrà creare automaticamente tabella hello in SQL Data Warehouse utilizzando lo schema di hello della tabella hello in origine hello archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d95b6-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="d95b6-113">Per informazioni dettagliate vedere [Creazione automatica della tabella](#auto-table-creation).</span><span class="sxs-lookup"><span data-stu-id="d95b6-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="d95b6-114">Tipo di autenticazione supportato</span><span class="sxs-lookup"><span data-stu-id="d95b6-114">Supported authentication type</span></span>
<span data-ttu-id="d95b6-115">È supportato il connettore Azure SQL Data Warehouse per l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="d95b6-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d95b6-116">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d95b6-116">Getting started</span></span>
<span data-ttu-id="d95b6-117">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un Azure SQL Data Warehouse usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="d95b6-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="d95b6-118">toocreate modo più semplice di Hello una pipeline che copia i dati da e verso Azure SQL Data Warehouse è toouse hello copia dati guidata.</span><span class="sxs-lookup"><span data-stu-id="d95b6-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="d95b6-119">Vedere [esercitazione: caricare i dati in SQL Data Warehouse con Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="d95b6-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="d95b6-120">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d95b6-121">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d95b6-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="d95b6-122">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="d95b6-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d95b6-123">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-123">Create a **data factory**.</span></span> <span data-ttu-id="d95b6-124">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="d95b6-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d95b6-125">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d95b6-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="d95b6-126">Ad esempio, se si copiano dati da un data warehouse di Azure blob storage tooan SQL di Azure, è creare due servizi collegati toolink l'account di archiviazione di Azure e la data factory di Azure SQL data warehouse tooyour.</span><span class="sxs-lookup"><span data-stu-id="d95b6-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="d95b6-127">Per le proprietà di servizio collegato che sono specifici tooAzure SQL Data Warehouse, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="d95b6-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="d95b6-128">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="d95b6-129">Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="d95b6-130">E si crea un altro set di dati nella tabella toospecify hello hello Azure SQL data warehouse contenente dati hello copiati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="d95b6-131">Per le proprietà di set di dati che sono specifici tooAzure SQL Data Warehouse, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="d95b6-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="d95b6-132">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="d95b6-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d95b6-133">Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e SqlDWSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="d95b6-134">Analogamente, se si sta copiando tooAzure Azure SQL Data Warehouse nell'archiviazione Blob, utilizzare SqlDWSource e BlobSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="d95b6-135">Per le proprietà di attività di copia che sono specifici tooAzure SQL Data Warehouse, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="d95b6-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d95b6-136">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d95b6-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="d95b6-137">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d95b6-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d95b6-138">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d95b6-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d95b6-139">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un Data Warehouse di SQL Azure, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d95b6-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="d95b6-140">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="d95b6-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d95b6-141">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="d95b6-141">Linked service properties</span></span>
<span data-ttu-id="d95b6-142">Hello nella tabella seguente fornisce una descrizione JSON tooAzure specifico di elementi del servizio collegato SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="d95b6-143">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d95b6-143">Property</span></span> | <span data-ttu-id="d95b6-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d95b6-144">Description</span></span> | <span data-ttu-id="d95b6-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d95b6-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d95b6-146">type</span><span class="sxs-lookup"><span data-stu-id="d95b6-146">type</span></span> |<span data-ttu-id="d95b6-147">proprietà di tipo Hello deve essere impostata su: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="d95b6-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="d95b6-148">Sì</span><span class="sxs-lookup"><span data-stu-id="d95b6-148">Yes</span></span> |
| <span data-ttu-id="d95b6-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="d95b6-149">connectionString</span></span> |<span data-ttu-id="d95b6-150">Specificare l'istanza di Azure SQL Data Warehouse toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="d95b6-151">È supportata solo l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="d95b6-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="d95b6-152">Sì</span><span class="sxs-lookup"><span data-stu-id="d95b6-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d95b6-153">Configurare [Firewall di Database SQL di Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e hello server di database troppo[consentire a servizi di Azure tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="d95b6-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="d95b6-154">Inoltre, se si copiano dati tooAzure SQL Data Warehouse da inclusi Azure esterno da origini dati locali con gateway factory di dati, configurare l'intervallo di indirizzi IP appropriata per la macchina hello che invia dati tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="d95b6-155">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="d95b6-155">Dataset properties</span></span>
<span data-ttu-id="d95b6-156">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d95b6-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d95b6-157">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="d95b6-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d95b6-158">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d95b6-159">Hello **typeProperties** sezione per hello set di dati di tipo **AzureSqlDWTable** è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d95b6-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="d95b6-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d95b6-160">Property</span></span> | <span data-ttu-id="d95b6-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d95b6-161">Description</span></span> | <span data-ttu-id="d95b6-162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d95b6-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d95b6-163">tableName</span><span class="sxs-lookup"><span data-stu-id="d95b6-163">tableName</span></span> |<span data-ttu-id="d95b6-164">Nome della tabella hello o della vista nel database di Azure SQL Data Warehouse hello che hello servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="d95b6-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="d95b6-165">Sì</span><span class="sxs-lookup"><span data-stu-id="d95b6-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d95b6-166">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="d95b6-166">Copy activity properties</span></span>
<span data-ttu-id="d95b6-167">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d95b6-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d95b6-168">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="d95b6-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="d95b6-169">Hello attività di copia accetta un solo input e produce un solo output.</span><span class="sxs-lookup"><span data-stu-id="d95b6-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="d95b6-170">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="d95b6-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d95b6-171">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="d95b6-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="d95b6-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="d95b6-172">SqlDWSource</span></span>
<span data-ttu-id="d95b6-173">Quando l'origine è di tipo **SqlDWSource**, hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="d95b6-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="d95b6-174">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d95b6-174">Property</span></span> | <span data-ttu-id="d95b6-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d95b6-175">Description</span></span> | <span data-ttu-id="d95b6-176">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d95b6-176">Allowed values</span></span> | <span data-ttu-id="d95b6-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d95b6-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d95b6-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d95b6-178">sqlReaderQuery</span></span> |<span data-ttu-id="d95b6-179">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d95b6-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d95b6-180">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="d95b6-180">SQL query string.</span></span> <span data-ttu-id="d95b6-181">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="d95b6-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="d95b6-182">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-182">No</span></span> |
| <span data-ttu-id="d95b6-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d95b6-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d95b6-184">Nome di hello stored procedure che legge i dati dalla tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="d95b6-185">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d95b6-185">Name of hello stored procedure.</span></span> <span data-ttu-id="d95b6-186">ultima istruzione SQL di Hello deve essere un'istruzione SELECT nella procedura hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="d95b6-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="d95b6-187">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-187">No</span></span> |
| <span data-ttu-id="d95b6-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d95b6-188">storedProcedureParameters</span></span> |<span data-ttu-id="d95b6-189">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d95b6-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d95b6-190">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="d95b6-190">Name/value pairs.</span></span> <span data-ttu-id="d95b6-191">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="d95b6-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d95b6-192">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-192">No</span></span> |

<span data-ttu-id="d95b6-193">Se hello **sqlReaderQuery** specificato per hello SqlDWSource, hello attività di copia viene eseguita questa query hello dati di Azure SQL Data Warehouse origine tooget hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="d95b6-194">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="d95b6-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="d95b6-195">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono utilizzati toobuild toorun una query su hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d95b6-196">Esempio: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="d95b6-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="d95b6-197">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="d95b6-198">Esempio SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="d95b6-198">SqlDWSource example</span></span>

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
<span data-ttu-id="d95b6-199">**definizione della stored procedure Hello archiviato:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="d95b6-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="d95b6-200">SqlDWSink</span></span>
<span data-ttu-id="d95b6-201">**SqlDWSink** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d95b6-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="d95b6-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d95b6-202">Property</span></span> | <span data-ttu-id="d95b6-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d95b6-203">Description</span></span> | <span data-ttu-id="d95b6-204">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d95b6-204">Allowed values</span></span> | <span data-ttu-id="d95b6-205">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d95b6-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d95b6-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d95b6-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d95b6-207">Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="d95b6-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="d95b6-208">Per informazioni dettagliate, vedere la sezione relativa alla [ripetibilità](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="d95b6-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="d95b6-209">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="d95b6-209">A query statement.</span></span> |<span data-ttu-id="d95b6-210">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-210">No</span></span> |
| <span data-ttu-id="d95b6-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="d95b6-211">allowPolyBase</span></span> |<span data-ttu-id="d95b6-212">Indica se toouse PolyBase (se applicabile) anziché meccanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="d95b6-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="d95b6-213">**Utilizzo di PolyBase è hello consigliato dei dati tooload in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="d95b6-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="d95b6-214">Vedere [dati tooload usare PolyBase in Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sezione per i vincoli e i dettagli.</span><span class="sxs-lookup"><span data-stu-id="d95b6-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="d95b6-215">True </span><span class="sxs-lookup"><span data-stu-id="d95b6-215">True</span></span> <br/><span data-ttu-id="d95b6-216">False (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="d95b6-216">False (default)</span></span> |<span data-ttu-id="d95b6-217">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-217">No</span></span> |
| <span data-ttu-id="d95b6-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="d95b6-218">polyBaseSettings</span></span> |<span data-ttu-id="d95b6-219">Un gruppo di proprietà che possono essere specificati quando hello **allowPolybase** impostata troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="d95b6-220">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-220">No</span></span> |
| <span data-ttu-id="d95b6-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="d95b6-221">rejectValue</span></span> |<span data-ttu-id="d95b6-222">Specifica il numero di hello o la percentuale di righe che può essere rifiutata prima di hello query ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d95b6-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="d95b6-223">Informazioni su ulteriori informazioni su del PolyBase hello rifiutare le opzioni di hello **argomenti** sezione [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="d95b6-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="d95b6-224">0 (impostazione predefinita), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="d95b6-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="d95b6-225">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-225">No</span></span> |
| <span data-ttu-id="d95b6-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="d95b6-226">rejectType</span></span> |<span data-ttu-id="d95b6-227">Specifica se l'opzione rejectValue hello è specificato come valore letterale o percentuale.</span><span class="sxs-lookup"><span data-stu-id="d95b6-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="d95b6-228">Value (impostazione predefinita), Percentage</span><span class="sxs-lookup"><span data-stu-id="d95b6-228">Value (default), Percentage</span></span> |<span data-ttu-id="d95b6-229">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-229">No</span></span> |
| <span data-ttu-id="d95b6-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="d95b6-230">rejectSampleValue</span></span> |<span data-ttu-id="d95b6-231">Determina il numero di hello di tooretrieve righe prima di hello PolyBase Ricalcola percentuale hello di righe rifiutate.</span><span class="sxs-lookup"><span data-stu-id="d95b6-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="d95b6-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="d95b6-232">1, 2, …</span></span> |<span data-ttu-id="d95b6-233">Sì se **rejectType** è **percentage**</span><span class="sxs-lookup"><span data-stu-id="d95b6-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="d95b6-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="d95b6-234">useTypeDefault</span></span> |<span data-ttu-id="d95b6-235">Specifica la modalità toohandle mancano i valori nel file di testo delimitati quando PolyBase recupera i dati da file di testo hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="d95b6-236">Altre informazioni su questa proprietà dalla sezione argomenti hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="d95b6-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="d95b6-237">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="d95b6-237">True, False (default)</span></span> |<span data-ttu-id="d95b6-238">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-238">No</span></span> |
| <span data-ttu-id="d95b6-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d95b6-239">writeBatchSize</span></span> |<span data-ttu-id="d95b6-240">Inserisce i dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello</span><span class="sxs-lookup"><span data-stu-id="d95b6-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="d95b6-241">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="d95b6-241">Integer (number of rows)</span></span> |<span data-ttu-id="d95b6-242">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-242">No (default: 10000)</span></span> |
| <span data-ttu-id="d95b6-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d95b6-243">writeBatchTimeout</span></span> |<span data-ttu-id="d95b6-244">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="d95b6-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="d95b6-245">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="d95b6-245">timespan</span></span><br/><br/> <span data-ttu-id="d95b6-246">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="d95b6-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d95b6-247">No</span><span class="sxs-lookup"><span data-stu-id="d95b6-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="d95b6-248">Esempio SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="d95b6-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="d95b6-249">Utilizzare i dati di PolyBase tooload in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d95b6-250">**[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** consente di caricare con efficacia grandi quantità di dati in Azure SQL Data Warehouse con una velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="d95b6-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="d95b6-251">È possibile visualizzare un miglioramento della velocità effettiva hello grandi dimensioni tramite PolyBase anziché meccanismo BULKINSERT di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="d95b6-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="d95b6-252">Vedere [Copiare il numero di riferimento prestazioni](data-factory-copy-activity-performance.md#performance-reference) con il confronto dettagliato.</span><span class="sxs-lookup"><span data-stu-id="d95b6-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="d95b6-253">Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="d95b6-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="d95b6-254">Se i dati di origine si trova in **Blob di Azure o archivio Azure Data Lake**e il formato di hello è compatibile con PolyBase, è possibile copiare direttamente tooAzure SQL Data Warehouse tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d95b6-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="d95b6-255">Vedere **[Copia diretta tramite PolyBase](#direct-copy-using-polybase)** con i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="d95b6-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="d95b6-256">Se l'archivio dati di origine e il formato non è supportata in origine da PolyBase, è possibile utilizzare hello  **[copia gestita usando PolyBase](#staged-copy-using-polybase)**  funzionalità alternativa.</span><span class="sxs-lookup"><span data-stu-id="d95b6-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="d95b6-257">Vengono inoltre una migliore velocità effettiva eseguendo automaticamente la conversione dei dati di hello nel formato compatibile con PolyBase e l'archiviazione dei dati di hello nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d95b6-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="d95b6-258">Vengono quindi caricati i dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="d95b6-259">Set hello `allowPolyBase` proprietà troppo**true** come illustrato nel seguente esempio per Data Factory di Azure toouse PolyBase toocopy dati in Azure SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d95b6-260">Quando si imposta allowPolyBase tootrue, è possibile specificare proprietà specifiche di PolyBase con hello `polyBaseSettings` gruppo di proprietà.</span><span class="sxs-lookup"><span data-stu-id="d95b6-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="d95b6-261">vedere hello [SqlDWSink](#SqlDWSink) per ulteriori informazioni sulle proprietà che è possibile utilizzare con impostazioni polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="d95b6-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="d95b6-262">Copia diretta tramite PolyBase</span><span class="sxs-lookup"><span data-stu-id="d95b6-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="d95b6-263">PolyBase di SQL Data Warehouse supporta direttamente Archiviazione BLOB di Azure e Azure Data Lake Store (mediante l'entità servizio) come origine e con requisiti di formato di file specifico.</span><span class="sxs-lookup"><span data-stu-id="d95b6-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="d95b6-264">Se i dati di origine soddisfino i criteri di hello descritti in questa sezione, è possibile copiare direttamente dall'origine dati archivio tooAzure che SQL Data Warehouse tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d95b6-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="d95b6-265">In caso contrario è possibile usare la [copia di staging tramite PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="d95b6-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="d95b6-266">toocopy dati dall'archivio Data Lake tooSQL Data Warehouse in modo efficiente, altre informazioni da [Data Factory di Azure rende anche più semplice e pratico toouncover informazioni significative dai dati quando si utilizza l'archivio Data Lake con SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="d95b6-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="d95b6-267">Se non vengono soddisfatti i requisiti di hello, Data Factory di Azure controlla le impostazioni di hello e passa automaticamente meccanismo BULKINSERT toohello per lo spostamento dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="d95b6-268">Il **servizio collegato all'origine** è di tipo: **AzureStorage** o **AzureDataLakeStore con autenticazione entità servizio**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="d95b6-269">Hello **set di dati input** è di tipo: **AzureBlob** o **AzureDataLakeStore**, e hello in tipo di formato `type` è di proprietà **OrcFormat** , o **TextFormat** con hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="d95b6-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="d95b6-270">`rowDelimiter` deve essere **\n**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="d95b6-271">`nullValue`è stato impostato troppo**una stringa vuota** (""), o `treatEmptyAsNull` è troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="d95b6-272">`encodingName`è stato impostato troppo**utf-8**, ovvero **predefinito** valore.</span><span class="sxs-lookup"><span data-stu-id="d95b6-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="d95b6-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` e `skipLineCount` non sono specificati.</span><span class="sxs-lookup"><span data-stu-id="d95b6-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="d95b6-274">`compression` può essere **no compression**, **GZip** o **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="d95b6-275">Non esiste alcun `skipHeaderLineCount` in **BlobSource** o **AzureDataLakeStore** per attività di copia nella pipeline hello hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="d95b6-276">Non esiste alcun `sliceIdentifierColumnName` in **SqlDWSink** per attività di copia nella pipeline hello hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="d95b6-277">PolyBase garantisce che tutti i dati verranno aggiornati o che nessun dato verrà aggiornato in una singola esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d95b6-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="d95b6-278">tooachieve **ripetibilità**, è possibile utilizzare `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="d95b6-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="d95b6-279">Non esiste alcun `columnMapping` utilizzata in hello associata nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d95b6-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="d95b6-280">copia di staging tramite PolyBase</span><span class="sxs-lookup"><span data-stu-id="d95b6-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="d95b6-281">Quando i dati di origine non soddisfano i criteri di hello introdotti nella sezione precedente di hello, è possibile abilitare una copia dei dati tramite un archivio di Blob di Azure staging provvisorio (non può essere archiviazione Premium).</span><span class="sxs-lookup"><span data-stu-id="d95b6-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="d95b6-282">In questo caso, Azure Data Factory automaticamente consente di eseguire trasformazioni hello dati toomeet dati formato requisiti di PolyBase, quindi utilizzare i dati di tooload PolyBase in SQL Data Warehouse e ultimo pulizia dei dati dall'archiviazione Blob hello temp.</span><span class="sxs-lookup"><span data-stu-id="d95b6-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="d95b6-283">Per informazioni dettagliate sul funzionamento generale della copia dei dati tramite un BLOB di Azure di staging, vedere la sezione [Copia di staging](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="d95b6-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="d95b6-284">Quando archiviano la copia di dati da un locale in Azure SQL Data Warehouse tramite PolyBase e sul gateway di gestione temporanea, se la versione del Gateway di gestione dati è di sotto di 2.4, è necessario JRE (Java Runtime Environment) del computer che viene utilizzato tootransform i dati di origine in formato corretto.</span><span class="sxs-lookup"><span data-stu-id="d95b6-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="d95b6-285">Suggerire che tooavoid più recente di toohello il gateway si aggiorna tale dipendenza.</span><span class="sxs-lookup"><span data-stu-id="d95b6-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="d95b6-286">toouse tale funzionalità, creare un [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) che fa riferimento l'Account di archiviazione di Azure che ha l'archiviazione blob provvisorio hello toohello, quindi specificare hello `enableStaging` e `stagingSettings` le proprietà per hello attività di copia come illustrato nel seguente codice hello:</span><span class="sxs-lookup"><span data-stu-id="d95b6-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="d95b6-287">Procedure consigliate per l'uso di PolyBase</span><span class="sxs-lookup"><span data-stu-id="d95b6-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="d95b6-288">Hello nelle sezioni seguenti forniscono ulteriori toohello consigliate migliore quelli citati in [procedure consigliate per Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="d95b6-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="d95b6-289">Autorizzazione database obbligatoria</span><span class="sxs-lookup"><span data-stu-id="d95b6-289">Required database permission</span></span>
<span data-ttu-id="d95b6-290">toouse PolyBase, è necessario hello utente viene utilizzato tooload dati in SQL Data Warehouse è hello [autorizzazione "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) nel database di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="d95b6-291">Unidirezionale tooachieve tooadd che tale utente come membro del ruolo "db_owner".</span><span class="sxs-lookup"><span data-stu-id="d95b6-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="d95b6-292">Informazioni su come toodo che seguendo [in questa sezione](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="d95b6-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="d95b6-293">Limitazione alle dimensioni di righe e al tipo di dati</span><span class="sxs-lookup"><span data-stu-id="d95b6-293">Row size and data type limitation</span></span>
<span data-ttu-id="d95b6-294">Carica Polybase è limitati tooloading righe sia inferiore a **1 MB** e non è possibile caricare tooVARCHR(MAX), nvarchar (max) o varbinary (max).</span><span class="sxs-lookup"><span data-stu-id="d95b6-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="d95b6-295">Fare riferimento troppo[qui](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="d95b6-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="d95b6-296">Se si dispone di dati di origine con le righe di dimensioni maggiori di 1 MB, è consigliabile tabelle di origine hello toosplit verticalmente in più piccole in hello riga massime di ognuno di essi non superi il limite di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="d95b6-297">le tabelle più piccole Hello possono quindi essere caricate usando PolyBase e uniti in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="d95b6-298">Classe di risorse di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="d95b6-299">tooachieve migliori prestazioni possibili, prendere in considerazione tooassign maggiori risorse classe toohello utente viene usato il tooload dati in SQL Data Warehouse tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d95b6-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="d95b6-300">Informazioni su come toodo che seguendo [un esempio di classe di risorse utente di modificare](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d95b6-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="d95b6-301">tableName in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d95b6-302">Hello nella tabella seguente vengono forniti esempi su come hello toospecify **tableName** proprietà nel set di dati JSON per diverse combinazioni di nome di tabella e dello schema.</span><span class="sxs-lookup"><span data-stu-id="d95b6-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="d95b6-303">Schema di database</span><span class="sxs-lookup"><span data-stu-id="d95b6-303">DB Schema</span></span> | <span data-ttu-id="d95b6-304">Nome tabella</span><span class="sxs-lookup"><span data-stu-id="d95b6-304">Table name</span></span> | <span data-ttu-id="d95b6-305">Proprietà JSON tableName</span><span class="sxs-lookup"><span data-stu-id="d95b6-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d95b6-306">dbo</span><span class="sxs-lookup"><span data-stu-id="d95b6-306">dbo</span></span> |<span data-ttu-id="d95b6-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="d95b6-307">MyTable</span></span> |<span data-ttu-id="d95b6-308">MyTable o dbo.MyTable o [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="d95b6-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="d95b6-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="d95b6-309">dbo1</span></span> |<span data-ttu-id="d95b6-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="d95b6-310">MyTable</span></span> |<span data-ttu-id="d95b6-311">dbo1.MyTable o [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="d95b6-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="d95b6-312">dbo</span><span class="sxs-lookup"><span data-stu-id="d95b6-312">dbo</span></span> |<span data-ttu-id="d95b6-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="d95b6-313">My.Table</span></span> |<span data-ttu-id="d95b6-314">[My.Table] o [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="d95b6-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="d95b6-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="d95b6-315">dbo1</span></span> |<span data-ttu-id="d95b6-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="d95b6-316">My.Table</span></span> |<span data-ttu-id="d95b6-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="d95b6-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="d95b6-318">Se viene visualizzato il seguente errore hello, può costituire un problema con il valore di hello che è specificato per la proprietà tableName di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="d95b6-319">Vedere la tabella hello per i valori di toospecify hello modo corretto per la proprietà di hello tableName JSON.</span><span class="sxs-lookup"><span data-stu-id="d95b6-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="d95b6-320">Colonne con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="d95b6-320">Columns with default values</span></span>
<span data-ttu-id="d95b6-321">Attualmente, PolyBase accetta solo funzionalità di Data Factory hello stesso numero di colonne come tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="d95b6-322">Se si ha una tabella con quattro colonne di cui una definita con un valore predefinito, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="d95b6-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="d95b6-323">dati di input Hello devono comunque contenere quattro colonne.</span><span class="sxs-lookup"><span data-stu-id="d95b6-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="d95b6-324">Fornisce un set di dati colonna 3 input produrrebbe un toohello simile di errore seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="d95b6-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="d95b6-325">Il valore NULL è una forma speciale di valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="d95b6-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="d95b6-326">Se la colonna hello ammette valori null, i dati di input di hello (in blob) per tale colonna potrebbe essere vuoti (non può essere mancante dal set di dati input hello).</span><span class="sxs-lookup"><span data-stu-id="d95b6-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="d95b6-327">PolyBase consente di inserire NULL relativa hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="d95b6-328">Creazione automatica della tabella</span><span class="sxs-lookup"><span data-stu-id="d95b6-328">Auto table creation</span></span>
<span data-ttu-id="d95b6-329">Se si utilizza Copia guidata toocopy dati da SQL Server o Database SQL di Azure tooAzure SQL Data Warehouse e hello tabella corrispondente toohello tabella di origine non esiste nell'archivio di destinazione hello, Data Factory può creare automaticamente tabella hello in hello del data warehouse con schema di tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="d95b6-330">Data Factory Crea tabella hello nell'archivio di destinazione hello con hello stesso nome nell'archivio dati di origine hello di tabella.</span><span class="sxs-lookup"><span data-stu-id="d95b6-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="d95b6-331">tipi di dati Hello per le colonne vengono scelti in base ai mapping dei tipi seguenti di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="d95b6-332">Se necessario, esegue toofix conversioni di tipo eventuali incompatibilità tra gli archivi di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d95b6-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="d95b6-333">Usa inoltre la distribuzione di tabella Round Robin.</span><span class="sxs-lookup"><span data-stu-id="d95b6-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="d95b6-334">Tipo di colonna di origine del Database SQL</span><span class="sxs-lookup"><span data-stu-id="d95b6-334">Source SQL Database column type</span></span> | <span data-ttu-id="d95b6-335">Tipo di colonna SQL DW di destinazione del Database (limitazione delle dimensioni)</span><span class="sxs-lookup"><span data-stu-id="d95b6-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="d95b6-336">int</span><span class="sxs-lookup"><span data-stu-id="d95b6-336">Int</span></span> | <span data-ttu-id="d95b6-337">int</span><span class="sxs-lookup"><span data-stu-id="d95b6-337">Int</span></span> |
| <span data-ttu-id="d95b6-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="d95b6-338">BigInt</span></span> | <span data-ttu-id="d95b6-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="d95b6-339">BigInt</span></span> |
| <span data-ttu-id="d95b6-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="d95b6-340">SmallInt</span></span> | <span data-ttu-id="d95b6-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="d95b6-341">SmallInt</span></span> |
| <span data-ttu-id="d95b6-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="d95b6-342">TinyInt</span></span> | <span data-ttu-id="d95b6-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="d95b6-343">TinyInt</span></span> |
| <span data-ttu-id="d95b6-344">Bit</span><span class="sxs-lookup"><span data-stu-id="d95b6-344">Bit</span></span> | <span data-ttu-id="d95b6-345">Bit</span><span class="sxs-lookup"><span data-stu-id="d95b6-345">Bit</span></span> |
| <span data-ttu-id="d95b6-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="d95b6-346">Decimal</span></span> | <span data-ttu-id="d95b6-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="d95b6-347">Decimal</span></span> |
| <span data-ttu-id="d95b6-348">Numeric</span><span class="sxs-lookup"><span data-stu-id="d95b6-348">Numeric</span></span> | <span data-ttu-id="d95b6-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="d95b6-349">Decimal</span></span> |
| <span data-ttu-id="d95b6-350">Float</span><span class="sxs-lookup"><span data-stu-id="d95b6-350">Float</span></span> | <span data-ttu-id="d95b6-351">Float</span><span class="sxs-lookup"><span data-stu-id="d95b6-351">Float</span></span> |
| <span data-ttu-id="d95b6-352">Money</span><span class="sxs-lookup"><span data-stu-id="d95b6-352">Money</span></span> | <span data-ttu-id="d95b6-353">Money</span><span class="sxs-lookup"><span data-stu-id="d95b6-353">Money</span></span> |
| <span data-ttu-id="d95b6-354">Real</span><span class="sxs-lookup"><span data-stu-id="d95b6-354">Real</span></span> | <span data-ttu-id="d95b6-355">Real</span><span class="sxs-lookup"><span data-stu-id="d95b6-355">Real</span></span> |
| <span data-ttu-id="d95b6-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="d95b6-356">SmallMoney</span></span> | <span data-ttu-id="d95b6-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="d95b6-357">SmallMoney</span></span> |
| <span data-ttu-id="d95b6-358">Binary</span><span class="sxs-lookup"><span data-stu-id="d95b6-358">Binary</span></span> | <span data-ttu-id="d95b6-359">Binary</span><span class="sxs-lookup"><span data-stu-id="d95b6-359">Binary</span></span> |
| <span data-ttu-id="d95b6-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="d95b6-360">Varbinary</span></span> | <span data-ttu-id="d95b6-361">Varbinary (backup too8000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="d95b6-362">Date</span><span class="sxs-lookup"><span data-stu-id="d95b6-362">Date</span></span> | <span data-ttu-id="d95b6-363">Data</span><span class="sxs-lookup"><span data-stu-id="d95b6-363">Date</span></span> |
| <span data-ttu-id="d95b6-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-364">DateTime</span></span> | <span data-ttu-id="d95b6-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-365">DateTime</span></span> |
| <span data-ttu-id="d95b6-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="d95b6-366">DateTime2</span></span> | <span data-ttu-id="d95b6-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="d95b6-367">DateTime2</span></span> |
| <span data-ttu-id="d95b6-368">Time</span><span class="sxs-lookup"><span data-stu-id="d95b6-368">Time</span></span> | <span data-ttu-id="d95b6-369">Time</span><span class="sxs-lookup"><span data-stu-id="d95b6-369">Time</span></span> |
| <span data-ttu-id="d95b6-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d95b6-370">DateTimeOffset</span></span> | <span data-ttu-id="d95b6-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d95b6-371">DateTimeOffset</span></span> |
| <span data-ttu-id="d95b6-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-372">SmallDateTime</span></span> | <span data-ttu-id="d95b6-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-373">SmallDateTime</span></span> |
| <span data-ttu-id="d95b6-374">Text</span><span class="sxs-lookup"><span data-stu-id="d95b6-374">Text</span></span> | <span data-ttu-id="d95b6-375">Varchar (backup too8000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="d95b6-376">NText</span><span class="sxs-lookup"><span data-stu-id="d95b6-376">NText</span></span> | <span data-ttu-id="d95b6-377">NVarChar (backup too4000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="d95b6-378">Image</span><span class="sxs-lookup"><span data-stu-id="d95b6-378">Image</span></span> | <span data-ttu-id="d95b6-379">VarBinary (backup too8000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="d95b6-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="d95b6-380">UniqueIdentifier</span></span> | <span data-ttu-id="d95b6-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="d95b6-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="d95b6-382">Char</span><span class="sxs-lookup"><span data-stu-id="d95b6-382">Char</span></span> | <span data-ttu-id="d95b6-383">Char</span><span class="sxs-lookup"><span data-stu-id="d95b6-383">Char</span></span> |
| <span data-ttu-id="d95b6-384">NChar</span><span class="sxs-lookup"><span data-stu-id="d95b6-384">NChar</span></span> | <span data-ttu-id="d95b6-385">NChar</span><span class="sxs-lookup"><span data-stu-id="d95b6-385">NChar</span></span> |
| <span data-ttu-id="d95b6-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="d95b6-386">VarChar</span></span> | <span data-ttu-id="d95b6-387">VarChar (backup too8000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="d95b6-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="d95b6-388">NVarChar</span></span> | <span data-ttu-id="d95b6-389">NVarChar (backup too4000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="d95b6-390">xml</span><span class="sxs-lookup"><span data-stu-id="d95b6-390">Xml</span></span> | <span data-ttu-id="d95b6-391">Varchar (backup too8000)</span><span class="sxs-lookup"><span data-stu-id="d95b6-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="d95b6-392">Mapping dei tipi per Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d95b6-393">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="d95b6-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="d95b6-394">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="d95b6-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="d95b6-395">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d95b6-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="d95b6-396">Quando si spostano dati troppo & da Azure SQL Data Warehouse, hello mapping seguenti vengono utilizzate dal tipo too.NET di tipo SQL e viceversa.</span><span class="sxs-lookup"><span data-stu-id="d95b6-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="d95b6-397">mapping di Hello è uguale a hello [mapping dei tipi di dati di SQL Server per ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="d95b6-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="d95b6-398">Tipo di motore di database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="d95b6-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="d95b6-399">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d95b6-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="d95b6-400">bigint</span><span class="sxs-lookup"><span data-stu-id="d95b6-400">bigint</span></span> |<span data-ttu-id="d95b6-401">Int64</span><span class="sxs-lookup"><span data-stu-id="d95b6-401">Int64</span></span> |
| <span data-ttu-id="d95b6-402">binary</span><span class="sxs-lookup"><span data-stu-id="d95b6-402">binary</span></span> |<span data-ttu-id="d95b6-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-403">Byte[]</span></span> |
| <span data-ttu-id="d95b6-404">bit</span><span class="sxs-lookup"><span data-stu-id="d95b6-404">bit</span></span> |<span data-ttu-id="d95b6-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="d95b6-405">Boolean</span></span> |
| <span data-ttu-id="d95b6-406">char</span><span class="sxs-lookup"><span data-stu-id="d95b6-406">char</span></span> |<span data-ttu-id="d95b6-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-407">String, Char[]</span></span> |
| <span data-ttu-id="d95b6-408">date</span><span class="sxs-lookup"><span data-stu-id="d95b6-408">date</span></span> |<span data-ttu-id="d95b6-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-409">DateTime</span></span> |
| <span data-ttu-id="d95b6-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-410">Datetime</span></span> |<span data-ttu-id="d95b6-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-411">DateTime</span></span> |
| <span data-ttu-id="d95b6-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="d95b6-412">datetime2</span></span> |<span data-ttu-id="d95b6-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-413">DateTime</span></span> |
| <span data-ttu-id="d95b6-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d95b6-414">Datetimeoffset</span></span> |<span data-ttu-id="d95b6-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d95b6-415">DateTimeOffset</span></span> |
| <span data-ttu-id="d95b6-416">Decimale</span><span class="sxs-lookup"><span data-stu-id="d95b6-416">Decimal</span></span> |<span data-ttu-id="d95b6-417">Decimale</span><span class="sxs-lookup"><span data-stu-id="d95b6-417">Decimal</span></span> |
| <span data-ttu-id="d95b6-418">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="d95b6-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="d95b6-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-419">Byte[]</span></span> |
| <span data-ttu-id="d95b6-420">Float</span><span class="sxs-lookup"><span data-stu-id="d95b6-420">Float</span></span> |<span data-ttu-id="d95b6-421">Double</span><span class="sxs-lookup"><span data-stu-id="d95b6-421">Double</span></span> |
| <span data-ttu-id="d95b6-422">immagine</span><span class="sxs-lookup"><span data-stu-id="d95b6-422">image</span></span> |<span data-ttu-id="d95b6-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-423">Byte[]</span></span> |
| <span data-ttu-id="d95b6-424">int</span><span class="sxs-lookup"><span data-stu-id="d95b6-424">int</span></span> |<span data-ttu-id="d95b6-425">Int32</span><span class="sxs-lookup"><span data-stu-id="d95b6-425">Int32</span></span> |
| <span data-ttu-id="d95b6-426">money</span><span class="sxs-lookup"><span data-stu-id="d95b6-426">money</span></span> |<span data-ttu-id="d95b6-427">Decimale</span><span class="sxs-lookup"><span data-stu-id="d95b6-427">Decimal</span></span> |
| <span data-ttu-id="d95b6-428">nchar</span><span class="sxs-lookup"><span data-stu-id="d95b6-428">nchar</span></span> |<span data-ttu-id="d95b6-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-429">String, Char[]</span></span> |
| <span data-ttu-id="d95b6-430">ntext</span><span class="sxs-lookup"><span data-stu-id="d95b6-430">ntext</span></span> |<span data-ttu-id="d95b6-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-431">String, Char[]</span></span> |
| <span data-ttu-id="d95b6-432">numeric</span><span class="sxs-lookup"><span data-stu-id="d95b6-432">numeric</span></span> |<span data-ttu-id="d95b6-433">Decimale</span><span class="sxs-lookup"><span data-stu-id="d95b6-433">Decimal</span></span> |
| <span data-ttu-id="d95b6-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="d95b6-434">nvarchar</span></span> |<span data-ttu-id="d95b6-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-435">String, Char[]</span></span> |
| <span data-ttu-id="d95b6-436">real</span><span class="sxs-lookup"><span data-stu-id="d95b6-436">real</span></span> |<span data-ttu-id="d95b6-437">Single</span><span class="sxs-lookup"><span data-stu-id="d95b6-437">Single</span></span> |
| <span data-ttu-id="d95b6-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="d95b6-438">rowversion</span></span> |<span data-ttu-id="d95b6-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-439">Byte[]</span></span> |
| <span data-ttu-id="d95b6-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="d95b6-440">smalldatetime</span></span> |<span data-ttu-id="d95b6-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="d95b6-441">DateTime</span></span> |
| <span data-ttu-id="d95b6-442">smallint</span><span class="sxs-lookup"><span data-stu-id="d95b6-442">smallint</span></span> |<span data-ttu-id="d95b6-443">Int16</span><span class="sxs-lookup"><span data-stu-id="d95b6-443">Int16</span></span> |
| <span data-ttu-id="d95b6-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="d95b6-444">smallmoney</span></span> |<span data-ttu-id="d95b6-445">Decimale</span><span class="sxs-lookup"><span data-stu-id="d95b6-445">Decimal</span></span> |
| <span data-ttu-id="d95b6-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="d95b6-446">sql_variant</span></span> |<span data-ttu-id="d95b6-447">Object *</span><span class="sxs-lookup"><span data-stu-id="d95b6-447">Object *</span></span> |
| <span data-ttu-id="d95b6-448">text</span><span class="sxs-lookup"><span data-stu-id="d95b6-448">text</span></span> |<span data-ttu-id="d95b6-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-449">String, Char[]</span></span> |
| <span data-ttu-id="d95b6-450">time</span><span class="sxs-lookup"><span data-stu-id="d95b6-450">time</span></span> |<span data-ttu-id="d95b6-451">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="d95b6-451">TimeSpan</span></span> |
| <span data-ttu-id="d95b6-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="d95b6-452">timestamp</span></span> |<span data-ttu-id="d95b6-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-453">Byte[]</span></span> |
| <span data-ttu-id="d95b6-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="d95b6-454">tinyint</span></span> |<span data-ttu-id="d95b6-455">Byte</span><span class="sxs-lookup"><span data-stu-id="d95b6-455">Byte</span></span> |
| <span data-ttu-id="d95b6-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="d95b6-456">uniqueidentifier</span></span> |<span data-ttu-id="d95b6-457">Guid</span><span class="sxs-lookup"><span data-stu-id="d95b6-457">Guid</span></span> |
| <span data-ttu-id="d95b6-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="d95b6-458">varbinary</span></span> |<span data-ttu-id="d95b6-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-459">Byte[]</span></span> |
| <span data-ttu-id="d95b6-460">varchar</span><span class="sxs-lookup"><span data-stu-id="d95b6-460">varchar</span></span> |<span data-ttu-id="d95b6-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="d95b6-461">String, Char[]</span></span> |
| <span data-ttu-id="d95b6-462">xml</span><span class="sxs-lookup"><span data-stu-id="d95b6-462">xml</span></span> |<span data-ttu-id="d95b6-463">xml</span><span class="sxs-lookup"><span data-stu-id="d95b6-463">Xml</span></span> |

<span data-ttu-id="d95b6-464">È anche possibile mappare le colonne di origine toocolumns di set di dati dal set di dati di sink nella definizione di attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="d95b6-465">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d95b6-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="d95b6-466">Esempi JSON per la copia di dati tooand da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="d95b6-467">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d95b6-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d95b6-468">Vengono visualizzate come toocopy tooand di dati da Azure SQL Data Warehouse e di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d95b6-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="d95b6-469">Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d95b6-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="d95b6-470">Esempio: Copiare i dati da Azure SQL Data Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d95b6-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="d95b6-471">esempio Hello definisce hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="d95b6-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="d95b6-472">Un servizio collegato di tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="d95b6-473">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d95b6-474">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d95b6-475">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d95b6-476">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlDWSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d95b6-477">esempio Hello copia dati della serie temporale (orari, giornalieri, ecc.) da una tabella nell'oggetto blob tooa database Azure SQL Data Warehouse ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d95b6-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="d95b6-478">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d95b6-479">**Servizio collegato di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="d95b6-480">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d95b6-481">**Set di dati di input di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="d95b6-482">esempio Hello presuppone di aver creato una tabella "MyTable" in Azure SQL Data Warehouse e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="d95b6-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d95b6-483">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="d95b6-484">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d95b6-485">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="d95b6-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d95b6-486">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="d95b6-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d95b6-487">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="d95b6-488">**Attività di copia in una pipeline con SqlDWSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="d95b6-489">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d95b6-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d95b6-490">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlDWSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d95b6-491">query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="d95b6-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="d95b6-492">Nell'esempio hello **sqlReaderQuery** specificato per hello SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="d95b6-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="d95b6-493">Hello attività di copia esegue query su dati di Azure SQL Data Warehouse origine tooget hello hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="d95b6-494">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="d95b6-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="d95b6-495">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono toobuild utilizzata una query (selezionare column1, column2 da mytable) toorun contro hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d95b6-496">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="d95b6-497">Esempio: Copiare i dati da tooAzure Blob di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d95b6-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="d95b6-498">esempio Hello definisce hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="d95b6-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="d95b6-499">Un servizio collegato di tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="d95b6-500">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d95b6-501">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d95b6-502">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="d95b6-503">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d95b6-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d95b6-504">esempio Hello copia dati della serie temporale (oraria, giornaliera, ecc.) dalla tabella tooa blob di Azure nel database di Azure SQL Data Warehouse ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d95b6-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="d95b6-505">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d95b6-506">**Servizio collegato di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="d95b6-507">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d95b6-508">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="d95b6-509">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="d95b6-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d95b6-510">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="d95b6-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d95b6-511">percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="d95b6-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="d95b6-512">"external": "true" impostazione informa il servizio di Data Factory hello che questa tabella è data factory di toohello esterni e non viene generata da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="d95b6-513">**Set di dati di output di Azure SQL Data Warehouse:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="d95b6-514">esempio Hello copia tabella tooa dati denominata "MyTable" in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d95b6-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d95b6-515">Creare la tabella hello in Azure SQL Data Warehouse con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello.</span><span class="sxs-lookup"><span data-stu-id="d95b6-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="d95b6-516">Aggiunta di nuove righe nella tabella toohello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d95b6-516">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="d95b6-517">**Copiare attività in una pipeline con BlobSource e SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="d95b6-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="d95b6-518">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d95b6-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d95b6-519">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="d95b6-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

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
<span data-ttu-id="d95b6-520">Per una procedura dettagliata, vedere hello [caricare 1 TB in Azure SQL Data Warehouse in 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md) e [caricano dati con Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) articolo hello Azure SQL Data Warehouse documentazione.</span><span class="sxs-lookup"><span data-stu-id="d95b6-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d95b6-521">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d95b6-521">Performance and Tuning</span></span>
<span data-ttu-id="d95b6-522">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="d95b6-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
