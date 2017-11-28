---
title: aaaMove dati da MySQL con Data Factory di Azure | Documenti Microsoft
description: Informazioni su come toomove dati da MySQL database usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="fb0fa-103">Spostare i dati da MySQL mediante Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="fb0fa-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="fb0fa-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="fb0fa-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="fb0fa-106">È possibile copiare dati da un archivio di dati di on-premise MySQL dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="fb0fa-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fb0fa-108">Data factory di attualmente supporta solo lo spostamento di dati da un MySQL archiviano tooother archivi di dati, ma non per lo spostamento dei dati da altro archivio dati di MySQL tooan di archivi di dati.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fb0fa-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fb0fa-109">Prerequisites</span></span>
<span data-ttu-id="fb0fa-110">Servizio Data Factory supporta origini di MySQL locale tooon connessione hello Gateway di gestione dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="fb0fa-111">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="fb0fa-112">Gateway è necessario anche se il database di MySQL hello è ospitato in una macchina virtuale IaaS di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="fb0fa-113">È possibile installare il gateway di hello in hello stessa macchina virtuale come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="fb0fa-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="fb0fa-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="fb0fa-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="fb0fa-115">Supported versions and installation</span></span>
<span data-ttu-id="fb0fa-116">Per Gateway di gestione dati tooconnect toohello MySQL Database, è necessario hello tooinstall [MySQL Connector/Net per Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versione 6.6.5 o versione successiva) hello nella stesso sistema come hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="fb0fa-117">Sono supportate le versioni di MySQL a partire dalla 5.1.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="fb0fa-118">Se si riscontra errori "Autenticazione non riuscita perché è chiuso parte remota hello flusso di trasporto hello.", è consigliabile hello tooupgrade versione toohigher MySQL Connector/Net.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fb0fa-119">introduttiva</span><span class="sxs-lookup"><span data-stu-id="fb0fa-119">Getting started</span></span>
<span data-ttu-id="fb0fa-120">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="fb0fa-121">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fb0fa-122">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="fb0fa-123">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fb0fa-124">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fb0fa-125">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb0fa-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="fb0fa-126">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fb0fa-127">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fb0fa-128">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fb0fa-129">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fb0fa-130">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fb0fa-131">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati di MySQL in locale, vedere [esempio JSON: copiare i dati da MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fb0fa-132">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa MySQL:</span><span class="sxs-lookup"><span data-stu-id="fb0fa-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fb0fa-133">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="fb0fa-133">Linked service properties</span></span>
<span data-ttu-id="fb0fa-134">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooMySQL collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="fb0fa-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fb0fa-135">Property</span></span> | <span data-ttu-id="fb0fa-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fb0fa-136">Description</span></span> | <span data-ttu-id="fb0fa-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fb0fa-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb0fa-138">type</span><span class="sxs-lookup"><span data-stu-id="fb0fa-138">type</span></span> |<span data-ttu-id="fb0fa-139">proprietà di tipo Hello deve essere impostata su: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="fb0fa-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="fb0fa-140">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-140">Yes</span></span> |
| <span data-ttu-id="fb0fa-141">server</span><span class="sxs-lookup"><span data-stu-id="fb0fa-141">server</span></span> |<span data-ttu-id="fb0fa-142">Nome del server MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="fb0fa-143">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-143">Yes</span></span> |
| <span data-ttu-id="fb0fa-144">database</span><span class="sxs-lookup"><span data-stu-id="fb0fa-144">database</span></span> |<span data-ttu-id="fb0fa-145">Nome del database MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="fb0fa-146">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-146">Yes</span></span> |
| <span data-ttu-id="fb0fa-147">schema</span><span class="sxs-lookup"><span data-stu-id="fb0fa-147">schema</span></span> |<span data-ttu-id="fb0fa-148">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="fb0fa-149">No</span><span class="sxs-lookup"><span data-stu-id="fb0fa-149">No</span></span> |
| <span data-ttu-id="fb0fa-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fb0fa-150">authenticationType</span></span> |<span data-ttu-id="fb0fa-151">Tipo di autenticazione usato toohello tooconnect di database MySQL.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="fb0fa-152">I valori possibili sono:`Basic`.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="fb0fa-153">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-153">Yes</span></span> |
| <span data-ttu-id="fb0fa-154">username</span><span class="sxs-lookup"><span data-stu-id="fb0fa-154">username</span></span> |<span data-ttu-id="fb0fa-155">Specificare i database di MySQL toohello tooconnect nome utente.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="fb0fa-156">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-156">Yes</span></span> |
| <span data-ttu-id="fb0fa-157">password</span><span class="sxs-lookup"><span data-stu-id="fb0fa-157">password</span></span> |<span data-ttu-id="fb0fa-158">Specificare la password per l'account utente di hello specificato.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="fb0fa-159">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-159">Yes</span></span> |
| <span data-ttu-id="fb0fa-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fb0fa-160">gatewayName</span></span> |<span data-ttu-id="fb0fa-161">Nome del gateway hello hello servizio Data Factory deve utilizzare database MySQL di tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="fb0fa-162">Sì</span><span class="sxs-lookup"><span data-stu-id="fb0fa-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="fb0fa-163">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="fb0fa-163">Dataset properties</span></span>
<span data-ttu-id="fb0fa-164">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fb0fa-165">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fb0fa-166">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fb0fa-167">sezione Hello typeProperties per set di dati di tipo **RelationalTable** (che include set di dati MySQL) ha le proprietà seguenti hello</span><span class="sxs-lookup"><span data-stu-id="fb0fa-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="fb0fa-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fb0fa-168">Property</span></span> | <span data-ttu-id="fb0fa-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fb0fa-169">Description</span></span> | <span data-ttu-id="fb0fa-170">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fb0fa-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb0fa-171">tableName</span><span class="sxs-lookup"><span data-stu-id="fb0fa-171">tableName</span></span> |<span data-ttu-id="fb0fa-172">Nome della tabella hello nell'istanza di MySQL Database che fa riferimento il servizio collegato a hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="fb0fa-173">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="fb0fa-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fb0fa-174">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="fb0fa-174">Copy activity properties</span></span>
<span data-ttu-id="fb0fa-175">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fb0fa-176">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="fb0fa-177">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="fb0fa-178">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fb0fa-179">Quando l'origine in attività di copia è di tipo **RelationalSource** (che include MySQL), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="fb0fa-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="fb0fa-180">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fb0fa-180">Property</span></span> | <span data-ttu-id="fb0fa-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fb0fa-181">Description</span></span> | <span data-ttu-id="fb0fa-182">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="fb0fa-182">Allowed values</span></span> | <span data-ttu-id="fb0fa-183">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fb0fa-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fb0fa-184">query</span><span class="sxs-lookup"><span data-stu-id="fb0fa-184">query</span></span> |<span data-ttu-id="fb0fa-185">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="fb0fa-186">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-186">SQL query string.</span></span> <span data-ttu-id="fb0fa-187">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="fb0fa-188">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="fb0fa-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="fb0fa-189">Esempio JSON: copiare i dati da MySQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="fb0fa-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="fb0fa-190">In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fb0fa-191">Viene illustrato come toocopy dati da un MySQL locale database tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="fb0fa-192">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb0fa-193">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="fb0fa-194">Non include istruzioni dettagliate per la creazione di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="fb0fa-195">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="fb0fa-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="fb0fa-196">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb0fa-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="fb0fa-197">Un servizio collegato di tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="fb0fa-198">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fb0fa-199">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fb0fa-200">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fb0fa-201">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fb0fa-202">esempio Hello copia dati da un risultato della query nel blob tooa di database MySQL ogni ora.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="fb0fa-203">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fb0fa-204">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="fb0fa-205">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fb0fa-206">**Servizio collegato MySQL**</span><span class="sxs-lookup"><span data-stu-id="fb0fa-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="fb0fa-207">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="fb0fa-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="fb0fa-208">**Set di dati di input MySQL**</span><span class="sxs-lookup"><span data-stu-id="fb0fa-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="fb0fa-209">esempio Hello presuppone aver creato una tabella "MyTable" di MySQL e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="fb0fa-210">L'impostazione "external": "true" informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
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

<span data-ttu-id="fb0fa-211">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="fb0fa-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fb0fa-212">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fb0fa-213">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fb0fa-214">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="fb0fa-215">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="fb0fa-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="fb0fa-216">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fb0fa-217">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fb0fa-218">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="fb0fa-219">Mapping dei tipi per MySQL</span><span class="sxs-lookup"><span data-stu-id="fb0fa-219">Type mapping for MySQL</span></span>
<span data-ttu-id="fb0fa-220">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="fb0fa-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="fb0fa-221">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="fb0fa-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fb0fa-222">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="fb0fa-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fb0fa-223">Quando si spostano dati tooMySQL, hello mapping seguenti vengono utilizzati dai tipi too.NET tipi di MySQL.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="fb0fa-224">Tipo di database MySQL</span><span class="sxs-lookup"><span data-stu-id="fb0fa-224">MySQL Database type</span></span> | <span data-ttu-id="fb0fa-225">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="fb0fa-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fb0fa-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="fb0fa-226">bigint unsigned</span></span> |<span data-ttu-id="fb0fa-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="fb0fa-227">Decimal</span></span> |
| <span data-ttu-id="fb0fa-228">bigint</span><span class="sxs-lookup"><span data-stu-id="fb0fa-228">bigint</span></span> |<span data-ttu-id="fb0fa-229">Int64</span><span class="sxs-lookup"><span data-stu-id="fb0fa-229">Int64</span></span> |
| <span data-ttu-id="fb0fa-230">Bit</span><span class="sxs-lookup"><span data-stu-id="fb0fa-230">bit</span></span> |<span data-ttu-id="fb0fa-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="fb0fa-231">Decimal</span></span> |
| <span data-ttu-id="fb0fa-232">BLOB</span><span class="sxs-lookup"><span data-stu-id="fb0fa-232">blob</span></span> |<span data-ttu-id="fb0fa-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fb0fa-233">Byte[]</span></span> |
| <span data-ttu-id="fb0fa-234">bool</span><span class="sxs-lookup"><span data-stu-id="fb0fa-234">bool</span></span> |<span data-ttu-id="fb0fa-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="fb0fa-235">Boolean</span></span> |
| <span data-ttu-id="fb0fa-236">char</span><span class="sxs-lookup"><span data-stu-id="fb0fa-236">char</span></span> |<span data-ttu-id="fb0fa-237">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-237">String</span></span> |
| <span data-ttu-id="fb0fa-238">date</span><span class="sxs-lookup"><span data-stu-id="fb0fa-238">date</span></span> |<span data-ttu-id="fb0fa-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="fb0fa-239">Datetime</span></span> |
| <span data-ttu-id="fb0fa-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="fb0fa-240">datetime</span></span> |<span data-ttu-id="fb0fa-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="fb0fa-241">Datetime</span></span> |
| <span data-ttu-id="fb0fa-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="fb0fa-242">decimal</span></span> |<span data-ttu-id="fb0fa-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="fb0fa-243">Decimal</span></span> |
| <span data-ttu-id="fb0fa-244">double precision</span><span class="sxs-lookup"><span data-stu-id="fb0fa-244">double precision</span></span> |<span data-ttu-id="fb0fa-245">Double</span><span class="sxs-lookup"><span data-stu-id="fb0fa-245">Double</span></span> |
| <span data-ttu-id="fb0fa-246">Double</span><span class="sxs-lookup"><span data-stu-id="fb0fa-246">double</span></span> |<span data-ttu-id="fb0fa-247">Double</span><span class="sxs-lookup"><span data-stu-id="fb0fa-247">Double</span></span> |
| <span data-ttu-id="fb0fa-248">enum</span><span class="sxs-lookup"><span data-stu-id="fb0fa-248">enum</span></span> |<span data-ttu-id="fb0fa-249">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-249">String</span></span> |
| <span data-ttu-id="fb0fa-250">float</span><span class="sxs-lookup"><span data-stu-id="fb0fa-250">float</span></span> |<span data-ttu-id="fb0fa-251">Single</span><span class="sxs-lookup"><span data-stu-id="fb0fa-251">Single</span></span> |
| <span data-ttu-id="fb0fa-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="fb0fa-252">int unsigned</span></span> |<span data-ttu-id="fb0fa-253">Int64</span><span class="sxs-lookup"><span data-stu-id="fb0fa-253">Int64</span></span> |
| <span data-ttu-id="fb0fa-254">int</span><span class="sxs-lookup"><span data-stu-id="fb0fa-254">int</span></span> |<span data-ttu-id="fb0fa-255">Int32</span><span class="sxs-lookup"><span data-stu-id="fb0fa-255">Int32</span></span> |
| <span data-ttu-id="fb0fa-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="fb0fa-256">integer unsigned</span></span> |<span data-ttu-id="fb0fa-257">Int64</span><span class="sxs-lookup"><span data-stu-id="fb0fa-257">Int64</span></span> |
| <span data-ttu-id="fb0fa-258">integer</span><span class="sxs-lookup"><span data-stu-id="fb0fa-258">integer</span></span> |<span data-ttu-id="fb0fa-259">Int32</span><span class="sxs-lookup"><span data-stu-id="fb0fa-259">Int32</span></span> |
| <span data-ttu-id="fb0fa-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="fb0fa-260">long varbinary</span></span> |<span data-ttu-id="fb0fa-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fb0fa-261">Byte[]</span></span> |
| <span data-ttu-id="fb0fa-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="fb0fa-262">long varchar</span></span> |<span data-ttu-id="fb0fa-263">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-263">String</span></span> |
| <span data-ttu-id="fb0fa-264">longblob</span><span class="sxs-lookup"><span data-stu-id="fb0fa-264">longblob</span></span> |<span data-ttu-id="fb0fa-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fb0fa-265">Byte[]</span></span> |
| <span data-ttu-id="fb0fa-266">longtext</span><span class="sxs-lookup"><span data-stu-id="fb0fa-266">longtext</span></span> |<span data-ttu-id="fb0fa-267">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-267">String</span></span> |
| <span data-ttu-id="fb0fa-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="fb0fa-268">mediumblob</span></span> |<span data-ttu-id="fb0fa-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fb0fa-269">Byte[]</span></span> |
| <span data-ttu-id="fb0fa-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="fb0fa-270">mediumint unsigned</span></span> |<span data-ttu-id="fb0fa-271">Int64</span><span class="sxs-lookup"><span data-stu-id="fb0fa-271">Int64</span></span> |
| <span data-ttu-id="fb0fa-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="fb0fa-272">mediumint</span></span> |<span data-ttu-id="fb0fa-273">Int32</span><span class="sxs-lookup"><span data-stu-id="fb0fa-273">Int32</span></span> |
| <span data-ttu-id="fb0fa-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="fb0fa-274">mediumtext</span></span> |<span data-ttu-id="fb0fa-275">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-275">String</span></span> |
| <span data-ttu-id="fb0fa-276">numeric</span><span class="sxs-lookup"><span data-stu-id="fb0fa-276">numeric</span></span> |<span data-ttu-id="fb0fa-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="fb0fa-277">Decimal</span></span> |
| <span data-ttu-id="fb0fa-278">real</span><span class="sxs-lookup"><span data-stu-id="fb0fa-278">real</span></span> |<span data-ttu-id="fb0fa-279">Double</span><span class="sxs-lookup"><span data-stu-id="fb0fa-279">Double</span></span> |
| <span data-ttu-id="fb0fa-280">set</span><span class="sxs-lookup"><span data-stu-id="fb0fa-280">set</span></span> |<span data-ttu-id="fb0fa-281">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-281">String</span></span> |
| <span data-ttu-id="fb0fa-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="fb0fa-282">smallint unsigned</span></span> |<span data-ttu-id="fb0fa-283">Int32</span><span class="sxs-lookup"><span data-stu-id="fb0fa-283">Int32</span></span> |
| <span data-ttu-id="fb0fa-284">smallint</span><span class="sxs-lookup"><span data-stu-id="fb0fa-284">smallint</span></span> |<span data-ttu-id="fb0fa-285">Int16</span><span class="sxs-lookup"><span data-stu-id="fb0fa-285">Int16</span></span> |
| <span data-ttu-id="fb0fa-286">text</span><span class="sxs-lookup"><span data-stu-id="fb0fa-286">text</span></span> |<span data-ttu-id="fb0fa-287">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-287">String</span></span> |
| <span data-ttu-id="fb0fa-288">time</span><span class="sxs-lookup"><span data-stu-id="fb0fa-288">time</span></span> |<span data-ttu-id="fb0fa-289">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="fb0fa-289">TimeSpan</span></span> |
| <span data-ttu-id="fb0fa-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="fb0fa-290">timestamp</span></span> |<span data-ttu-id="fb0fa-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="fb0fa-291">Datetime</span></span> |
| <span data-ttu-id="fb0fa-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="fb0fa-292">tinyblob</span></span> |<span data-ttu-id="fb0fa-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fb0fa-293">Byte[]</span></span> |
| <span data-ttu-id="fb0fa-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="fb0fa-294">tinyint unsigned</span></span> |<span data-ttu-id="fb0fa-295">Int16</span><span class="sxs-lookup"><span data-stu-id="fb0fa-295">Int16</span></span> |
| <span data-ttu-id="fb0fa-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="fb0fa-296">tinyint</span></span> |<span data-ttu-id="fb0fa-297">Int16</span><span class="sxs-lookup"><span data-stu-id="fb0fa-297">Int16</span></span> |
| <span data-ttu-id="fb0fa-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="fb0fa-298">tinytext</span></span> |<span data-ttu-id="fb0fa-299">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-299">String</span></span> |
| <span data-ttu-id="fb0fa-300">varchar</span><span class="sxs-lookup"><span data-stu-id="fb0fa-300">varchar</span></span> |<span data-ttu-id="fb0fa-301">String</span><span class="sxs-lookup"><span data-stu-id="fb0fa-301">String</span></span> |
| <span data-ttu-id="fb0fa-302">year</span><span class="sxs-lookup"><span data-stu-id="fb0fa-302">year</span></span> |<span data-ttu-id="fb0fa-303">int</span><span class="sxs-lookup"><span data-stu-id="fb0fa-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fb0fa-304">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="fb0fa-304">Map source toosink columns</span></span>
<span data-ttu-id="fb0fa-305">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="fb0fa-306">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="fb0fa-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="fb0fa-307">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fb0fa-308">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fb0fa-309">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fb0fa-310">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fb0fa-311">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fb0fa-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fb0fa-312">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="fb0fa-312">Performance and Tuning</span></span>
<span data-ttu-id="fb0fa-313">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="fb0fa-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
