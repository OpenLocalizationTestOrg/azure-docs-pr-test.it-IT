---
title: dati aaaMove da Teradata usando Azure Data Factory | Documenti Microsoft
description: Altre informazioni sul connettore di Teradata per hello servizio Data Factory che consente di spostare i dati da Teradata Database
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="e363c-103">Spostare i dati da Teradata utilizzando Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="e363c-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="e363c-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="e363c-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="e363c-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="e363c-106">È possibile copiare dati da un archivio di dati di on-premise Teradata dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="e363c-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="e363c-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="e363c-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e363c-108">Data factory di attualmente supporta solo lo spostamento di dati da un Teradata archiviano tooother archivi di dati, ma non per lo spostamento dei dati dall'archivio di dati altri dati archivi tooa Teradata.</span><span class="sxs-lookup"><span data-stu-id="e363c-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e363c-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e363c-109">Prerequisites</span></span>
<span data-ttu-id="e363c-110">Data factory di supporta origini di Teradata locale tooon connessione tramite Gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="e363c-111">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="e363c-112">Anche se hello Teradata è ospitato in una macchina virtuale IaaS di Azure, è necessario gateway.</span><span class="sxs-lookup"><span data-stu-id="e363c-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="e363c-113">È possibile installare il gateway di hello in hello stessa VM IaaS come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="e363c-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="e363c-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="e363c-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e363c-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="e363c-115">Supported versions and installation</span></span>
<span data-ttu-id="e363c-116">Per Gateway di gestione dati tooconnect toohello Teradata Database, è necessario tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versione 14 o sopra in hello stesso sistema come hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="e363c-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="e363c-117">Sono supportate le versioni di Teradata a partire dalla 12.</span><span class="sxs-lookup"><span data-stu-id="e363c-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e363c-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e363c-118">Getting started</span></span>
<span data-ttu-id="e363c-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="e363c-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="e363c-120">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="e363c-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e363c-121">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="e363c-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="e363c-122">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="e363c-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e363c-123">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="e363c-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e363c-124">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="e363c-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="e363c-125">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="e363c-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e363c-126">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e363c-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="e363c-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e363c-128">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="e363c-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e363c-129">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e363c-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e363c-130">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio di dati Teradata locale, vedere [esempio JSON: copiare i dati da tooAzure Teradata Blob](#json-example-copy-data-from-teradata-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e363c-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e363c-131">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa Teradata:</span><span class="sxs-lookup"><span data-stu-id="e363c-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e363c-132">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="e363c-132">Linked service properties</span></span>
<span data-ttu-id="e363c-133">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooTeradata collegato gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="e363c-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="e363c-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e363c-134">Property</span></span> | <span data-ttu-id="e363c-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e363c-135">Description</span></span> | <span data-ttu-id="e363c-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e363c-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e363c-137">type</span><span class="sxs-lookup"><span data-stu-id="e363c-137">type</span></span> |<span data-ttu-id="e363c-138">proprietà di tipo Hello deve essere impostata su: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="e363c-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="e363c-139">Sì</span><span class="sxs-lookup"><span data-stu-id="e363c-139">Yes</span></span> |
| <span data-ttu-id="e363c-140">server</span><span class="sxs-lookup"><span data-stu-id="e363c-140">server</span></span> |<span data-ttu-id="e363c-141">Nome del server Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="e363c-142">Sì</span><span class="sxs-lookup"><span data-stu-id="e363c-142">Yes</span></span> |
| <span data-ttu-id="e363c-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e363c-143">authenticationType</span></span> |<span data-ttu-id="e363c-144">Tipo di autenticazione usato tooconnect toohello Teradata database.</span><span class="sxs-lookup"><span data-stu-id="e363c-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="e363c-145">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="e363c-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e363c-146">Sì</span><span class="sxs-lookup"><span data-stu-id="e363c-146">Yes</span></span> |
| <span data-ttu-id="e363c-147">username</span><span class="sxs-lookup"><span data-stu-id="e363c-147">username</span></span> |<span data-ttu-id="e363c-148">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="e363c-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e363c-149">No</span><span class="sxs-lookup"><span data-stu-id="e363c-149">No</span></span> |
| <span data-ttu-id="e363c-150">password</span><span class="sxs-lookup"><span data-stu-id="e363c-150">password</span></span> |<span data-ttu-id="e363c-151">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e363c-152">No</span><span class="sxs-lookup"><span data-stu-id="e363c-152">No</span></span> |
| <span data-ttu-id="e363c-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e363c-153">gatewayName</span></span> |<span data-ttu-id="e363c-154">Nome del gateway hello hello servizio Data Factory deve usare database di Teradata tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="e363c-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="e363c-155">Sì</span><span class="sxs-lookup"><span data-stu-id="e363c-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e363c-156">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="e363c-156">Dataset properties</span></span>
<span data-ttu-id="e363c-157">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e363c-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e363c-158">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="e363c-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e363c-159">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e363c-160">Non sono attualmente presenti proprietà del tipo non supportato per i set di dati Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e363c-161">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="e363c-161">Copy activity properties</span></span>
<span data-ttu-id="e363c-162">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e363c-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e363c-163">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="e363c-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="e363c-164">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="e363c-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e363c-165">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="e363c-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e363c-166">Quando origine hello è di tipo **RelationalSource** (che include Teradata), hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="e363c-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e363c-167">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e363c-167">Property</span></span> | <span data-ttu-id="e363c-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e363c-168">Description</span></span> | <span data-ttu-id="e363c-169">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="e363c-169">Allowed values</span></span> | <span data-ttu-id="e363c-170">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e363c-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e363c-171">query</span><span class="sxs-lookup"><span data-stu-id="e363c-171">query</span></span> |<span data-ttu-id="e363c-172">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e363c-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e363c-173">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="e363c-173">SQL query string.</span></span> <span data-ttu-id="e363c-174">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="e363c-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="e363c-175">Sì</span><span class="sxs-lookup"><span data-stu-id="e363c-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="e363c-176">Esempio JSON: copiare i dati da tooAzure Teradata Blob</span><span class="sxs-lookup"><span data-stu-id="e363c-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="e363c-177">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e363c-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e363c-178">Vengono visualizzate come dati toocopy tooAzure Teradata nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="e363c-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="e363c-179">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e363c-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="e363c-180">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="e363c-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="e363c-181">Un servizio collegato di tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e363c-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="e363c-182">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e363c-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e363c-183">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e363c-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="e363c-184">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e363c-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e363c-185">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e363c-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e363c-186">esempio Hello copia dati da un risultato di query nell'oggetto blob tooa Teradata database ogni ora.</span><span class="sxs-lookup"><span data-stu-id="e363c-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="e363c-187">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e363c-188">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="e363c-189">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e363c-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="e363c-190">**Servizio collegato Teradata:**</span><span class="sxs-lookup"><span data-stu-id="e363c-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="e363c-191">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="e363c-191">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="e363c-192">**Set di dati di input Teradata:**</span><span class="sxs-lookup"><span data-stu-id="e363c-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="e363c-193">esempio Hello presuppone aver creato una tabella "MyTable" in Teradata e contiene una colonna denominata "timestamp" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="e363c-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="e363c-194">L'impostazione "external": true informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="e363c-195">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="e363c-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e363c-196">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="e363c-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e363c-197">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="e363c-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e363c-198">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="e363c-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="e363c-199">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="e363c-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e363c-200">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e si svolge ogni ora toorun pianificato.</span><span class="sxs-lookup"><span data-stu-id="e363c-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="e363c-201">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e363c-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="e363c-202">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="e363c-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="e363c-203">Mapping dei tipi per Teradata</span><span class="sxs-lookup"><span data-stu-id="e363c-203">Type mapping for Teradata</span></span>
<span data-ttu-id="e363c-204">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo hello attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="e363c-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="e363c-205">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="e363c-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e363c-206">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="e363c-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e363c-207">Quando si spostano dati tooTeradata, hello mapping seguenti vengono utilizzati dal tipo too.NET di tipo Teradata.</span><span class="sxs-lookup"><span data-stu-id="e363c-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="e363c-208">Tipo di database Teradata</span><span class="sxs-lookup"><span data-stu-id="e363c-208">Teradata Database type</span></span> | <span data-ttu-id="e363c-209">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e363c-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="e363c-210">Char</span><span class="sxs-lookup"><span data-stu-id="e363c-210">Char</span></span> |<span data-ttu-id="e363c-211">String</span><span class="sxs-lookup"><span data-stu-id="e363c-211">String</span></span> |
| <span data-ttu-id="e363c-212">Clob</span><span class="sxs-lookup"><span data-stu-id="e363c-212">Clob</span></span> |<span data-ttu-id="e363c-213">String</span><span class="sxs-lookup"><span data-stu-id="e363c-213">String</span></span> |
| <span data-ttu-id="e363c-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="e363c-214">Graphic</span></span> |<span data-ttu-id="e363c-215">String</span><span class="sxs-lookup"><span data-stu-id="e363c-215">String</span></span> |
| <span data-ttu-id="e363c-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="e363c-216">VarChar</span></span> |<span data-ttu-id="e363c-217">String</span><span class="sxs-lookup"><span data-stu-id="e363c-217">String</span></span> |
| <span data-ttu-id="e363c-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="e363c-218">VarGraphic</span></span> |<span data-ttu-id="e363c-219">String</span><span class="sxs-lookup"><span data-stu-id="e363c-219">String</span></span> |
| <span data-ttu-id="e363c-220">BLOB</span><span class="sxs-lookup"><span data-stu-id="e363c-220">Blob</span></span> |<span data-ttu-id="e363c-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e363c-221">Byte[]</span></span> |
| <span data-ttu-id="e363c-222">Byte</span><span class="sxs-lookup"><span data-stu-id="e363c-222">Byte</span></span> |<span data-ttu-id="e363c-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e363c-223">Byte[]</span></span> |
| <span data-ttu-id="e363c-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="e363c-224">VarByte</span></span> |<span data-ttu-id="e363c-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e363c-225">Byte[]</span></span> |
| <span data-ttu-id="e363c-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="e363c-226">BigInt</span></span> |<span data-ttu-id="e363c-227">Int64</span><span class="sxs-lookup"><span data-stu-id="e363c-227">Int64</span></span> |
| <span data-ttu-id="e363c-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="e363c-228">ByteInt</span></span> |<span data-ttu-id="e363c-229">Int16</span><span class="sxs-lookup"><span data-stu-id="e363c-229">Int16</span></span> |
| <span data-ttu-id="e363c-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="e363c-230">Decimal</span></span> |<span data-ttu-id="e363c-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="e363c-231">Decimal</span></span> |
| <span data-ttu-id="e363c-232">Double</span><span class="sxs-lookup"><span data-stu-id="e363c-232">Double</span></span> |<span data-ttu-id="e363c-233">Double</span><span class="sxs-lookup"><span data-stu-id="e363c-233">Double</span></span> |
| <span data-ttu-id="e363c-234">Integer</span><span class="sxs-lookup"><span data-stu-id="e363c-234">Integer</span></span> |<span data-ttu-id="e363c-235">Int32</span><span class="sxs-lookup"><span data-stu-id="e363c-235">Int32</span></span> |
| <span data-ttu-id="e363c-236">Number</span><span class="sxs-lookup"><span data-stu-id="e363c-236">Number</span></span> |<span data-ttu-id="e363c-237">Double</span><span class="sxs-lookup"><span data-stu-id="e363c-237">Double</span></span> |
| <span data-ttu-id="e363c-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="e363c-238">SmallInt</span></span> |<span data-ttu-id="e363c-239">Int16</span><span class="sxs-lookup"><span data-stu-id="e363c-239">Int16</span></span> |
| <span data-ttu-id="e363c-240">Date</span><span class="sxs-lookup"><span data-stu-id="e363c-240">Date</span></span> |<span data-ttu-id="e363c-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="e363c-241">DateTime</span></span> |
| <span data-ttu-id="e363c-242">Time</span><span class="sxs-lookup"><span data-stu-id="e363c-242">Time</span></span> |<span data-ttu-id="e363c-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-243">TimeSpan</span></span> |
| <span data-ttu-id="e363c-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="e363c-244">Time With Time Zone</span></span> |<span data-ttu-id="e363c-245">String</span><span class="sxs-lookup"><span data-stu-id="e363c-245">String</span></span> |
| <span data-ttu-id="e363c-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e363c-246">Timestamp</span></span> |<span data-ttu-id="e363c-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="e363c-247">DateTime</span></span> |
| <span data-ttu-id="e363c-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="e363c-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="e363c-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="e363c-249">DateTimeOffset</span></span> |
| <span data-ttu-id="e363c-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="e363c-250">Interval Day</span></span> |<span data-ttu-id="e363c-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-251">TimeSpan</span></span> |
| <span data-ttu-id="e363c-252">Intervallo giorno tooHour</span><span class="sxs-lookup"><span data-stu-id="e363c-252">Interval Day tooHour</span></span> |<span data-ttu-id="e363c-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-253">TimeSpan</span></span> |
| <span data-ttu-id="e363c-254">Intervallo giorno tooMinute</span><span class="sxs-lookup"><span data-stu-id="e363c-254">Interval Day tooMinute</span></span> |<span data-ttu-id="e363c-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-255">TimeSpan</span></span> |
| <span data-ttu-id="e363c-256">Intervallo giorno tooSecond</span><span class="sxs-lookup"><span data-stu-id="e363c-256">Interval Day tooSecond</span></span> |<span data-ttu-id="e363c-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-257">TimeSpan</span></span> |
| <span data-ttu-id="e363c-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="e363c-258">Interval Hour</span></span> |<span data-ttu-id="e363c-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-259">TimeSpan</span></span> |
| <span data-ttu-id="e363c-260">Intervallo ora tooMinute</span><span class="sxs-lookup"><span data-stu-id="e363c-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="e363c-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-261">TimeSpan</span></span> |
| <span data-ttu-id="e363c-262">Intervallo ora tooSecond</span><span class="sxs-lookup"><span data-stu-id="e363c-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="e363c-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-263">TimeSpan</span></span> |
| <span data-ttu-id="e363c-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="e363c-264">Interval Minute</span></span> |<span data-ttu-id="e363c-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-265">TimeSpan</span></span> |
| <span data-ttu-id="e363c-266">TooSecond minuti di intervallo</span><span class="sxs-lookup"><span data-stu-id="e363c-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="e363c-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-267">TimeSpan</span></span> |
| <span data-ttu-id="e363c-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="e363c-268">Interval Second</span></span> |<span data-ttu-id="e363c-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e363c-269">TimeSpan</span></span> |
| <span data-ttu-id="e363c-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="e363c-270">Interval Year</span></span> |<span data-ttu-id="e363c-271">String</span><span class="sxs-lookup"><span data-stu-id="e363c-271">String</span></span> |
| <span data-ttu-id="e363c-272">Intervallo anno tooMonth</span><span class="sxs-lookup"><span data-stu-id="e363c-272">Interval Year tooMonth</span></span> |<span data-ttu-id="e363c-273">String</span><span class="sxs-lookup"><span data-stu-id="e363c-273">String</span></span> |
| <span data-ttu-id="e363c-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="e363c-274">Interval Month</span></span> |<span data-ttu-id="e363c-275">String</span><span class="sxs-lookup"><span data-stu-id="e363c-275">String</span></span> |
| <span data-ttu-id="e363c-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="e363c-276">Period(Date)</span></span> |<span data-ttu-id="e363c-277">String</span><span class="sxs-lookup"><span data-stu-id="e363c-277">String</span></span> |
| <span data-ttu-id="e363c-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="e363c-278">Period(Time)</span></span> |<span data-ttu-id="e363c-279">String</span><span class="sxs-lookup"><span data-stu-id="e363c-279">String</span></span> |
| <span data-ttu-id="e363c-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="e363c-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="e363c-281">String</span><span class="sxs-lookup"><span data-stu-id="e363c-281">String</span></span> |
| <span data-ttu-id="e363c-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="e363c-282">Period(Timestamp)</span></span> |<span data-ttu-id="e363c-283">String</span><span class="sxs-lookup"><span data-stu-id="e363c-283">String</span></span> |
| <span data-ttu-id="e363c-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="e363c-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="e363c-285">String</span><span class="sxs-lookup"><span data-stu-id="e363c-285">String</span></span> |
| <span data-ttu-id="e363c-286">Xml</span><span class="sxs-lookup"><span data-stu-id="e363c-286">Xml</span></span> |<span data-ttu-id="e363c-287">String</span><span class="sxs-lookup"><span data-stu-id="e363c-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="e363c-288">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="e363c-288">Map source toosink columns</span></span>
<span data-ttu-id="e363c-289">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e363c-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e363c-290">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="e363c-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="e363c-291">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="e363c-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e363c-292">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="e363c-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e363c-293">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="e363c-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e363c-294">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="e363c-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e363c-295">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="e363c-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e363c-296">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="e363c-296">Performance and Tuning</span></span>
<span data-ttu-id="e363c-297">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="e363c-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
