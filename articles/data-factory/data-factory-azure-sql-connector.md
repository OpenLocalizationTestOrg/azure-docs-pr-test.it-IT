---
title: aaaCopy dati da e verso il Database SQL di Azure | Documenti Microsoft
description: Informazioni su come toocopy dati da e verso il Database SQL di Azure usando Azure Data Factory.
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
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="b5930-103">Copia dati tooand dal Database di SQL Azure con Data Factory di Azure</span><span class="sxs-lookup"><span data-stu-id="b5930-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="b5930-104">Questo articolo spiega come toouse hello attività di copia in Azure Data Factory toomove dati tooand dal Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b5930-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="b5930-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="b5930-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="b5930-106">Supported scenarios</span></span>
<span data-ttu-id="b5930-107">È possibile copiare dati **dal Database di SQL Azure** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5930-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b5930-108">È possibile copiare dati da archivi dati seguenti hello **tooAzure Database SQL**:</span><span class="sxs-lookup"><span data-stu-id="b5930-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="b5930-109">Tipo di autenticazione supportato</span><span class="sxs-lookup"><span data-stu-id="b5930-109">Supported authentication type</span></span>
<span data-ttu-id="b5930-110">Il connettore per database SQL di Azure supporta l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="b5930-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b5930-111">Introduzione</span><span class="sxs-lookup"><span data-stu-id="b5930-111">Getting started</span></span>
<span data-ttu-id="b5930-112">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un database SQL di Azure usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="b5930-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="b5930-113">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="b5930-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b5930-114">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="b5930-115">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="b5930-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b5930-116">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="b5930-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b5930-117">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5930-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="b5930-118">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="b5930-118">Create a **data factory**.</span></span> <span data-ttu-id="b5930-119">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="b5930-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b5930-120">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="b5930-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="b5930-121">Ad esempio, se si copiano dati da un database di SQL Azure tooan di archiviazione blob di Azure, è creare due servizi collegati toolink l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="b5930-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="b5930-122">Per le proprietà di servizio collegato che sono tooAzure specifico Database SQL, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="b5930-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="b5930-123">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="b5930-124">Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="b5930-125">E, alla creazione di un altro set di dati toospecify hello SQL nella tabella nel database di SQL Azure hello che contiene dati hello copiati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="b5930-126">Per le proprietà di set di dati che sono specifici tooAzure archivio Data Lake, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="b5930-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="b5930-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="b5930-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b5930-128">Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e di SqlSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="b5930-129">Analogamente, se si sta copiando tooAzure Database SQL di Azure nell'archiviazione Blob, utilizzare SqlSource e BlobSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="b5930-130">Per le proprietà di attività di copia che sono specifici tooAzure Database SQL, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="b5930-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b5930-131">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="b5930-132">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="b5930-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="b5930-133">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5930-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="b5930-134">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un Database di SQL Azure, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-sql-database) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b5930-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="b5930-135">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure Database SQL:</span><span class="sxs-lookup"><span data-stu-id="b5930-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="b5930-136">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="b5930-136">Linked service properties</span></span>
<span data-ttu-id="b5930-137">SQL Azure collegato collegamenti al servizio una data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="b5930-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="b5930-138">Hello nella tabella seguente fornisce una descrizione per JSON elementi specifici tooAzure SQL servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b5930-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="b5930-139">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b5930-139">Property</span></span> | <span data-ttu-id="b5930-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5930-140">Description</span></span> | <span data-ttu-id="b5930-141">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b5930-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5930-142">type</span><span class="sxs-lookup"><span data-stu-id="b5930-142">type</span></span> |<span data-ttu-id="b5930-143">proprietà di tipo Hello deve essere impostata su: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="b5930-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="b5930-144">Sì</span><span class="sxs-lookup"><span data-stu-id="b5930-144">Yes</span></span> |
| <span data-ttu-id="b5930-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="b5930-145">connectionString</span></span> |<span data-ttu-id="b5930-146">Specificare l'istanza del Database di SQL Azure toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="b5930-147">È supportata solo l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="b5930-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="b5930-148">Sì</span><span class="sxs-lookup"><span data-stu-id="b5930-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="b5930-149">Configurare [Firewall di Database SQL di Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello server di database troppo[consentire a servizi di Azure tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="b5930-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="b5930-150">Inoltre, se si copiano dati tooAzure Database SQL da inclusi Azure esterno da origini dati locali con gateway factory di dati, configurare l'intervallo di indirizzi IP appropriata per la macchina hello che invia dati tooAzure Database SQL.</span><span class="sxs-lookup"><span data-stu-id="b5930-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="b5930-151">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="b5930-151">Dataset properties</span></span>
<span data-ttu-id="b5930-152">toospecify toorepresent un set di dati dati di input o outpui in un database SQL di Azure, impostare proprietà di tipo hello del set di dati hello: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="b5930-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="b5930-153">Set hello **linkedServiceName** proprietà del nome di toohello hello set di dati di SQL Azure hello servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b5930-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="b5930-154">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b5930-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b5930-155">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="b5930-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b5930-156">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b5930-157">Hello **typeProperties** sezione per hello set di dati di tipo **AzureSqlTable** è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5930-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="b5930-158">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b5930-158">Property</span></span> | <span data-ttu-id="b5930-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5930-159">Description</span></span> | <span data-ttu-id="b5930-160">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b5930-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5930-161">tableName</span><span class="sxs-lookup"><span data-stu-id="b5930-161">tableName</span></span> |<span data-ttu-id="b5930-162">Nome della tabella hello o della vista nell'istanza di Database SQL di Azure hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="b5930-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="b5930-163">Sì</span><span class="sxs-lookup"><span data-stu-id="b5930-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b5930-164">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="b5930-164">Copy activity properties</span></span>
<span data-ttu-id="b5930-165">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b5930-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b5930-166">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="b5930-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="b5930-167">Hello attività di copia accetta un solo input e produce un solo output.</span><span class="sxs-lookup"><span data-stu-id="b5930-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="b5930-168">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="b5930-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="b5930-169">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="b5930-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="b5930-170">Se si spostano dati da un database SQL di Azure, impostare il tipo di origine di hello nell'attività di copia hello troppo**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="b5930-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="b5930-171">Analogamente, se si stanno spostando i database SQL di Azure tooan di dati, impostare il tipo di sink hello nell'attività di copia hello troppo**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="b5930-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="b5930-172">Questa sezione presenta un elenco delle proprietà supportate da SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="b5930-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="b5930-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="b5930-173">SqlSource</span></span>
<span data-ttu-id="b5930-174">Nell'attività di copia, l'origine hello è di tipo **SqlSource**, hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="b5930-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="b5930-175">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b5930-175">Property</span></span> | <span data-ttu-id="b5930-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5930-176">Description</span></span> | <span data-ttu-id="b5930-177">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="b5930-177">Allowed values</span></span> | <span data-ttu-id="b5930-178">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b5930-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b5930-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="b5930-179">sqlReaderQuery</span></span> |<span data-ttu-id="b5930-180">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b5930-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="b5930-181">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="b5930-181">SQL query string.</span></span> <span data-ttu-id="b5930-182">Esempio: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="b5930-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="b5930-183">No</span><span class="sxs-lookup"><span data-stu-id="b5930-183">No</span></span> |
| <span data-ttu-id="b5930-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="b5930-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="b5930-185">Nome di hello stored procedure che legge i dati dalla tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="b5930-186">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-186">Name of hello stored procedure.</span></span> <span data-ttu-id="b5930-187">ultima istruzione SQL di Hello deve essere un'istruzione SELECT nella procedura hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="b5930-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="b5930-188">No</span><span class="sxs-lookup"><span data-stu-id="b5930-188">No</span></span> |
| <span data-ttu-id="b5930-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="b5930-189">storedProcedureParameters</span></span> |<span data-ttu-id="b5930-190">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="b5930-191">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="b5930-191">Name/value pairs.</span></span> <span data-ttu-id="b5930-192">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="b5930-193">No</span><span class="sxs-lookup"><span data-stu-id="b5930-193">No</span></span> |

<span data-ttu-id="b5930-194">Se hello **sqlReaderQuery** specificato per hello SqlSource, hello attività di copia viene eseguita questa query hello Database SQL di Azure tooget hello dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="b5930-195">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="b5930-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="b5930-196">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono toobuild utilizzata una query (`select column1, column2 from mytable`) toorun contro hello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5930-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="b5930-197">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="b5930-198">Quando si utilizza **sqlReaderStoredProcedureName**, è comunque necessario toospecify un valore per hello **tableName** proprietà hello set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="b5930-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="b5930-199">Non sono disponibili convalide eseguite su questa tabella.</span><span class="sxs-lookup"><span data-stu-id="b5930-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="b5930-200">Esempio SqlSource</span><span class="sxs-lookup"><span data-stu-id="b5930-200">SqlSource example</span></span>

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

<span data-ttu-id="b5930-201">**definizione della stored procedure Hello archiviato:**</span><span class="sxs-lookup"><span data-stu-id="b5930-201">**hello stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="b5930-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="b5930-202">SqlSink</span></span>
<span data-ttu-id="b5930-203">**SqlSink** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5930-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="b5930-204">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b5930-204">Property</span></span> | <span data-ttu-id="b5930-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5930-205">Description</span></span> | <span data-ttu-id="b5930-206">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="b5930-206">Allowed values</span></span> | <span data-ttu-id="b5930-207">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b5930-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b5930-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="b5930-208">writeBatchTimeout</span></span> |<span data-ttu-id="b5930-209">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="b5930-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="b5930-210">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="b5930-210">timespan</span></span><br/><br/> <span data-ttu-id="b5930-211">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="b5930-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="b5930-212">No</span><span class="sxs-lookup"><span data-stu-id="b5930-212">No</span></span> |
| <span data-ttu-id="b5930-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="b5930-213">writeBatchSize</span></span> |<span data-ttu-id="b5930-214">Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="b5930-215">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="b5930-215">Integer (number of rows)</span></span> |<span data-ttu-id="b5930-216">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="b5930-216">No (default: 10000)</span></span> |
| <span data-ttu-id="b5930-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="b5930-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="b5930-218">Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="b5930-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="b5930-219">Per altre informazioni, vedere la [copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="b5930-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="b5930-220">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="b5930-220">A query statement.</span></span> |<span data-ttu-id="b5930-221">No</span><span class="sxs-lookup"><span data-stu-id="b5930-221">No</span></span> |
| <span data-ttu-id="b5930-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="b5930-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="b5930-223">Specificare un nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b5930-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="b5930-224">Per altre informazioni, vedere la [copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="b5930-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="b5930-225">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="b5930-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="b5930-226">No</span><span class="sxs-lookup"><span data-stu-id="b5930-226">No</span></span> |
| <span data-ttu-id="b5930-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="b5930-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="b5930-228">Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="b5930-229">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="b5930-230">No</span><span class="sxs-lookup"><span data-stu-id="b5930-230">No</span></span> |
| <span data-ttu-id="b5930-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="b5930-231">storedProcedureParameters</span></span> |<span data-ttu-id="b5930-232">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="b5930-233">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="b5930-233">Name/value pairs.</span></span> <span data-ttu-id="b5930-234">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="b5930-235">No</span><span class="sxs-lookup"><span data-stu-id="b5930-235">No</span></span> |
| <span data-ttu-id="b5930-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="b5930-236">sqlWriterTableType</span></span> |<span data-ttu-id="b5930-237">Specificare un toobe nome tipo di tabella utilizzati in hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="b5930-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="b5930-238">Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati.</span><span class="sxs-lookup"><span data-stu-id="b5930-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="b5930-239">Codice della stored procedure può unire dati hello copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="b5930-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="b5930-240">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="b5930-240">A table type name.</span></span> |<span data-ttu-id="b5930-241">No</span><span class="sxs-lookup"><span data-stu-id="b5930-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="b5930-242">Esempio SqlSink</span><span class="sxs-lookup"><span data-stu-id="b5930-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="b5930-243">Esempi JSON per la copia dei dati tooand dal Database SQL</span><span class="sxs-lookup"><span data-stu-id="b5930-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="b5930-244">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b5930-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b5930-245">Vengono visualizzate come toocopy tooand di dati dal Database di SQL Azure e archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5930-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="b5930-246">Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5930-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="b5930-247">Esempio: Copiare i dati da Database SQL di Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="b5930-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="b5930-248">Hello stesso definisce hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="b5930-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="b5930-249">Un servizio collegato di tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="b5930-250">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b5930-251">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b5930-252">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b5930-253">Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b5930-254">esempio Hello copia dati della serie temporale (oraria, giornaliera, ecc.) da una tabella in blob tooa di database SQL di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5930-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="b5930-255">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="b5930-256">**Servizio collegato per il database SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="b5930-257">Vedere hello [servizio collegato di Azure SQL](#linked-service) sezione per hello elenco delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b5930-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="b5930-258">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="b5930-259">Vedere hello [Blob di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) articolo per elenco hello delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b5930-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="b5930-260">**Set di dati di input SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="b5930-261">esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Azure e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="b5930-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="b5930-262">L'impostazione "external": "true" informa il servizio di Azure Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="b5930-263">Vedere hello [proprietà del tipo di set di dati SQL di Azure](#dataset) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="b5930-264">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b5930-265">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="b5930-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b5930-266">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="b5930-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b5930-267">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="b5930-268">Vedere hello [proprietà del tipo di set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="b5930-269">**Un'attività di copia in una pipeline con un'origine SQL e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="b5930-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="b5930-270">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5930-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="b5930-271">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b5930-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="b5930-272">query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="b5930-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="b5930-273">Nell'esempio hello **sqlReaderQuery** specificato per hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="b5930-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="b5930-274">Attività di copia Hello consente di eseguire questa query hello dati hello tooget origine di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5930-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="b5930-275">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="b5930-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="b5930-276">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono utilizzati toobuild toorun una query sul Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="b5930-277">Ad esempio: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="b5930-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="b5930-278">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="b5930-279">Vedere hello [origine Sql](#sqlsource) sezione e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) per elenco hello delle proprietà supportate da SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="b5930-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="b5930-280">Esempio: Copiare i dati da Blob di Azure tooAzure Database SQL</span><span class="sxs-lookup"><span data-stu-id="b5930-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="b5930-281">esempio Hello definisce hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="b5930-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="b5930-282">Un servizio collegato di tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="b5930-283">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b5930-284">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b5930-285">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="b5930-286">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b5930-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b5930-287">esempio Hello copia dati della serie temporale (oraria, giornaliera, ecc.) dalla tabella tooa blob di Azure nel database SQL di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5930-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="b5930-288">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="b5930-289">**Servizio collegato SQL di Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="b5930-290">Vedere hello [servizio collegato di Azure SQL](#linked-service) sezione per hello elenco delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b5930-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="b5930-291">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="b5930-292">Vedere hello [Blob di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) articolo per elenco hello delle proprietà supportate da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b5930-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="b5930-293">**Set di dati di input del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="b5930-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="b5930-294">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="b5930-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b5930-295">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="b5930-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b5930-296">percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="b5930-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="b5930-297">"external": "true" impostazione informa il servizio di Data Factory hello che questa tabella è data factory di toohello esterni e non viene generata da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="b5930-298">Vedere hello [proprietà del tipo di set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="b5930-299">**Set di dati di aoutput del database SQL di Azure**</span><span class="sxs-lookup"><span data-stu-id="b5930-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="b5930-300">esempio Hello copia tabella tooa dati denominata "MyTable" in SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b5930-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="b5930-301">Creare la tabella hello in SQL Azure con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="b5930-302">Aggiunta di nuove righe nella tabella toohello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5930-302">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="b5930-303">Vedere hello [proprietà del tipo di set di dati SQL di Azure](#dataset) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="b5930-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="b5930-304">**Un'attività di copia in una pipeline con un'origine BLOB e un sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="b5930-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="b5930-305">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5930-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="b5930-306">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="b5930-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
<span data-ttu-id="b5930-307">Vedere hello [Sql Sink](#sqlsink) sezione e [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) per elenco hello delle proprietà supportate da SqlSink e BlobSource.</span><span class="sxs-lookup"><span data-stu-id="b5930-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="b5930-308">Colonne Identity nel database di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="b5930-308">Identity columns in hello target database</span></span>
<span data-ttu-id="b5930-309">In questa sezione viene fornito un esempio per la copia di dati da una tabella di origine senza una tabella di destinazione tooa colonna identity con una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="b5930-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="b5930-310">**Tabella di origine:**</span><span class="sxs-lookup"><span data-stu-id="b5930-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="b5930-311">**Tabella di destinazione:**</span><span class="sxs-lookup"><span data-stu-id="b5930-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="b5930-312">Si noti che la tabella di destinazione hello include una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="b5930-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="b5930-313">**Definizione JSON del set di dati di origine**</span><span class="sxs-lookup"><span data-stu-id="b5930-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="b5930-314">**Definizione JSON del set di dati di destinazione**</span><span class="sxs-lookup"><span data-stu-id="b5930-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="b5930-315">Si noti che la tabella di origine e la tabella di destinazione hanno schemi diversi (la destinazione include una colonna aggiuntiva identity).</span><span class="sxs-lookup"><span data-stu-id="b5930-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="b5930-316">In questo scenario, è necessario toospecify **struttura** proprietà nella definizione di set di dati destinazione hello, che non include una colonna identity hello.</span><span class="sxs-lookup"><span data-stu-id="b5930-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="b5930-317">Chiamare una stored procedure da un sink SQL</span><span class="sxs-lookup"><span data-stu-id="b5930-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="b5930-318">Per un esempio di come chiamare una stored procedure da un sink SQL in un'attività di copia di una pipeline, vedere l'articolo su come [richiamare una stored procedure per il sink SQL nell'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="b5930-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="b5930-319">Mapping dei tipi per il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b5930-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="b5930-320">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="b5930-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="b5930-321">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="b5930-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="b5930-322">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="b5930-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="b5930-323">Quando si spostano dati tooand dal Database SQL di Azure, hello mapping seguenti vengono utilizzate dal tipo too.NET di tipo SQL e viceversa.</span><span class="sxs-lookup"><span data-stu-id="b5930-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="b5930-324">mapping di Hello è identico a hello mapping dei tipi di dati di SQL Server per ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="b5930-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="b5930-325">Tipo di motore di database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="b5930-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="b5930-326">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b5930-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b5930-327">bigint</span><span class="sxs-lookup"><span data-stu-id="b5930-327">bigint</span></span> |<span data-ttu-id="b5930-328">Int64</span><span class="sxs-lookup"><span data-stu-id="b5930-328">Int64</span></span> |
| <span data-ttu-id="b5930-329">binary</span><span class="sxs-lookup"><span data-stu-id="b5930-329">binary</span></span> |<span data-ttu-id="b5930-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5930-330">Byte[]</span></span> |
| <span data-ttu-id="b5930-331">bit</span><span class="sxs-lookup"><span data-stu-id="b5930-331">bit</span></span> |<span data-ttu-id="b5930-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="b5930-332">Boolean</span></span> |
| <span data-ttu-id="b5930-333">char</span><span class="sxs-lookup"><span data-stu-id="b5930-333">char</span></span> |<span data-ttu-id="b5930-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b5930-334">String, Char[]</span></span> |
| <span data-ttu-id="b5930-335">date</span><span class="sxs-lookup"><span data-stu-id="b5930-335">date</span></span> |<span data-ttu-id="b5930-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5930-336">DateTime</span></span> |
| <span data-ttu-id="b5930-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5930-337">Datetime</span></span> |<span data-ttu-id="b5930-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5930-338">DateTime</span></span> |
| <span data-ttu-id="b5930-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="b5930-339">datetime2</span></span> |<span data-ttu-id="b5930-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5930-340">DateTime</span></span> |
| <span data-ttu-id="b5930-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b5930-341">Datetimeoffset</span></span> |<span data-ttu-id="b5930-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b5930-342">DateTimeOffset</span></span> |
| <span data-ttu-id="b5930-343">Decimale</span><span class="sxs-lookup"><span data-stu-id="b5930-343">Decimal</span></span> |<span data-ttu-id="b5930-344">Decimale</span><span class="sxs-lookup"><span data-stu-id="b5930-344">Decimal</span></span> |
| <span data-ttu-id="b5930-345">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="b5930-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="b5930-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5930-346">Byte[]</span></span> |
| <span data-ttu-id="b5930-347">Float</span><span class="sxs-lookup"><span data-stu-id="b5930-347">Float</span></span> |<span data-ttu-id="b5930-348">Double</span><span class="sxs-lookup"><span data-stu-id="b5930-348">Double</span></span> |
| <span data-ttu-id="b5930-349">immagine</span><span class="sxs-lookup"><span data-stu-id="b5930-349">image</span></span> |<span data-ttu-id="b5930-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5930-350">Byte[]</span></span> |
| <span data-ttu-id="b5930-351">int</span><span class="sxs-lookup"><span data-stu-id="b5930-351">int</span></span> |<span data-ttu-id="b5930-352">Int32</span><span class="sxs-lookup"><span data-stu-id="b5930-352">Int32</span></span> |
| <span data-ttu-id="b5930-353">money</span><span class="sxs-lookup"><span data-stu-id="b5930-353">money</span></span> |<span data-ttu-id="b5930-354">Decimale</span><span class="sxs-lookup"><span data-stu-id="b5930-354">Decimal</span></span> |
| <span data-ttu-id="b5930-355">nchar</span><span class="sxs-lookup"><span data-stu-id="b5930-355">nchar</span></span> |<span data-ttu-id="b5930-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b5930-356">String, Char[]</span></span> |
| <span data-ttu-id="b5930-357">ntext</span><span class="sxs-lookup"><span data-stu-id="b5930-357">ntext</span></span> |<span data-ttu-id="b5930-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b5930-358">String, Char[]</span></span> |
| <span data-ttu-id="b5930-359">numeric</span><span class="sxs-lookup"><span data-stu-id="b5930-359">numeric</span></span> |<span data-ttu-id="b5930-360">Decimale</span><span class="sxs-lookup"><span data-stu-id="b5930-360">Decimal</span></span> |
| <span data-ttu-id="b5930-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="b5930-361">nvarchar</span></span> |<span data-ttu-id="b5930-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b5930-362">String, Char[]</span></span> |
| <span data-ttu-id="b5930-363">real</span><span class="sxs-lookup"><span data-stu-id="b5930-363">real</span></span> |<span data-ttu-id="b5930-364">Single</span><span class="sxs-lookup"><span data-stu-id="b5930-364">Single</span></span> |
| <span data-ttu-id="b5930-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="b5930-365">rowversion</span></span> |<span data-ttu-id="b5930-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5930-366">Byte[]</span></span> |
| <span data-ttu-id="b5930-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="b5930-367">smalldatetime</span></span> |<span data-ttu-id="b5930-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="b5930-368">DateTime</span></span> |
| <span data-ttu-id="b5930-369">smallint</span><span class="sxs-lookup"><span data-stu-id="b5930-369">smallint</span></span> |<span data-ttu-id="b5930-370">Int16</span><span class="sxs-lookup"><span data-stu-id="b5930-370">Int16</span></span> |
| <span data-ttu-id="b5930-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="b5930-371">smallmoney</span></span> |<span data-ttu-id="b5930-372">Decimale</span><span class="sxs-lookup"><span data-stu-id="b5930-372">Decimal</span></span> |
| <span data-ttu-id="b5930-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="b5930-373">sql_variant</span></span> |<span data-ttu-id="b5930-374">Object *</span><span class="sxs-lookup"><span data-stu-id="b5930-374">Object *</span></span> |
| <span data-ttu-id="b5930-375">text</span><span class="sxs-lookup"><span data-stu-id="b5930-375">text</span></span> |<span data-ttu-id="b5930-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b5930-376">String, Char[]</span></span> |
| <span data-ttu-id="b5930-377">time</span><span class="sxs-lookup"><span data-stu-id="b5930-377">time</span></span> |<span data-ttu-id="b5930-378">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="b5930-378">TimeSpan</span></span> |
| <span data-ttu-id="b5930-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="b5930-379">timestamp</span></span> |<span data-ttu-id="b5930-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5930-380">Byte[]</span></span> |
| <span data-ttu-id="b5930-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="b5930-381">tinyint</span></span> |<span data-ttu-id="b5930-382">Byte</span><span class="sxs-lookup"><span data-stu-id="b5930-382">Byte</span></span> |
| <span data-ttu-id="b5930-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="b5930-383">uniqueidentifier</span></span> |<span data-ttu-id="b5930-384">Guid</span><span class="sxs-lookup"><span data-stu-id="b5930-384">Guid</span></span> |
| <span data-ttu-id="b5930-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="b5930-385">varbinary</span></span> |<span data-ttu-id="b5930-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5930-386">Byte[]</span></span> |
| <span data-ttu-id="b5930-387">varchar</span><span class="sxs-lookup"><span data-stu-id="b5930-387">varchar</span></span> |<span data-ttu-id="b5930-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b5930-388">String, Char[]</span></span> |
| <span data-ttu-id="b5930-389">xml</span><span class="sxs-lookup"><span data-stu-id="b5930-389">xml</span></span> |<span data-ttu-id="b5930-390">xml</span><span class="sxs-lookup"><span data-stu-id="b5930-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="b5930-391">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="b5930-391">Map source toosink columns</span></span>
<span data-ttu-id="b5930-392">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b5930-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="b5930-393">Copia ripetibile</span><span class="sxs-lookup"><span data-stu-id="b5930-393">Repeatable copy</span></span>
<span data-ttu-id="b5930-394">Quando si copiano dati tooSQL Database del Server, attività di copia hello Accoda tabella di dati toohello sink per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b5930-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="b5930-395">Vedere invece tooperform UPSERT [tooSqlSink scrittura Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) articolo.</span><span class="sxs-lookup"><span data-stu-id="b5930-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="b5930-396">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="b5930-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="b5930-397">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="b5930-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b5930-398">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="b5930-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b5930-399">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="b5930-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b5930-400">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b5930-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b5930-401">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b5930-401">Performance and Tuning</span></span>
<span data-ttu-id="b5930-402">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="b5930-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
