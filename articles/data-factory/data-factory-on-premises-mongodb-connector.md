---
title: dati aaaMove MongoDB mediante Data Factory | Documenti Microsoft
description: Informazioni su come dati toomove MongoDB database usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="dee21-103">Spostare i dati da MongoDB con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="dee21-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="dee21-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database di MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="dee21-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="dee21-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="dee21-106">È possibile copiare dati da un archivio di dati di on-premise MongoDB dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="dee21-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="dee21-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="dee21-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="dee21-108">Data factory di attualmente supporta solo lo spostamento di dati da un MongoDB archiviano tooother archivi di dati, ma non per lo spostamento dei dati dall'archivio dati di MongoDB altri dati archivi tooan.</span><span class="sxs-lookup"><span data-stu-id="dee21-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dee21-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dee21-109">Prerequisites</span></span>
<span data-ttu-id="dee21-110">Per hello Azure Data Factory servizio toobe tooconnect in grado di tooyour MongoDB database locale, è necessario installare hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="dee21-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="dee21-111">Le versioni MongoDB supportate sono 2.4, 2.6, 3.0 e 3.2.</span><span class="sxs-lookup"><span data-stu-id="dee21-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="dee21-112">Gateway di gestione di dati in hello nello stesso computer che ospita il database hello o tooavoid un computer separato competono per le risorse con i database di hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="dee21-113">Gateway di gestione dati è un software che si connette a servizi di toocloud origini dati locali in modo sicuro e gestito.</span><span class="sxs-lookup"><span data-stu-id="dee21-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="dee21-114">Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="dee21-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="dee21-115">Vedere [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate sulla configurazione di gateway hello una pipeline di dati toomove dati.</span><span class="sxs-lookup"><span data-stu-id="dee21-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="dee21-116">Quando si installa il gateway di hello, viene automaticamente installato un tooMongoDB tooconnect di MongoDB Microsoft ODBC driver utilizzato.</span><span class="sxs-lookup"><span data-stu-id="dee21-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dee21-117">È necessario toouse hello gateway tooconnect tooMongoDB anche se è ospitato in macchine virtuali IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="dee21-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="dee21-118">Se si sta tentando di istanza tooan tooconnect MongoDB ospitato nel cloud, è possibile installare anche l'istanza del gateway hello in hello VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="dee21-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="dee21-119">introduttiva</span><span class="sxs-lookup"><span data-stu-id="dee21-119">Getting started</span></span>
<span data-ttu-id="dee21-120">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un archivio dati MongoDB usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="dee21-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="dee21-121">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="dee21-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="dee21-122">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="dee21-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="dee21-123">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="dee21-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="dee21-124">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="dee21-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="dee21-125">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="dee21-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="dee21-126">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="dee21-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="dee21-127">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="dee21-128">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="dee21-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="dee21-129">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="dee21-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="dee21-130">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dee21-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="dee21-131">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati di MongoDB locale, vedere [esempio JSON: copiare i dati da tooAzure MongoDB Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="dee21-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="dee21-132">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono utilizzati toodefine Data Factory entità specifiche tooMongoDB origine:</span><span class="sxs-lookup"><span data-stu-id="dee21-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="dee21-133">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="dee21-133">Linked service properties</span></span>
<span data-ttu-id="dee21-134">Hello seguente tabella fornisce una descrizione per gli elementi JSON specifici troppo**OnPremisesMongoDB** servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="dee21-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="dee21-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dee21-135">Property</span></span> | <span data-ttu-id="dee21-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dee21-136">Description</span></span> | <span data-ttu-id="dee21-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dee21-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dee21-138">type</span><span class="sxs-lookup"><span data-stu-id="dee21-138">type</span></span> |<span data-ttu-id="dee21-139">proprietà di tipo Hello deve essere impostata su: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="dee21-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="dee21-140">Sì</span><span class="sxs-lookup"><span data-stu-id="dee21-140">Yes</span></span> |
| <span data-ttu-id="dee21-141">server</span><span class="sxs-lookup"><span data-stu-id="dee21-141">server</span></span> |<span data-ttu-id="dee21-142">IP il nome host o indirizzo del server di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="dee21-143">Sì</span><span class="sxs-lookup"><span data-stu-id="dee21-143">Yes</span></span> |
| <span data-ttu-id="dee21-144">port</span><span class="sxs-lookup"><span data-stu-id="dee21-144">port</span></span> |<span data-ttu-id="dee21-145">La porta TCP che hello MongoDB server utilizza toolisten per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="dee21-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="dee21-146">Facoltativo, valore predefinito: 27017</span><span class="sxs-lookup"><span data-stu-id="dee21-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="dee21-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="dee21-147">authenticationType</span></span> |<span data-ttu-id="dee21-148">Di base o anonima.</span><span class="sxs-lookup"><span data-stu-id="dee21-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="dee21-149">Sì</span><span class="sxs-lookup"><span data-stu-id="dee21-149">Yes</span></span> |
| <span data-ttu-id="dee21-150">username</span><span class="sxs-lookup"><span data-stu-id="dee21-150">username</span></span> |<span data-ttu-id="dee21-151">Utente account tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dee21-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="dee21-152">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="dee21-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="dee21-153">password</span><span class="sxs-lookup"><span data-stu-id="dee21-153">password</span></span> |<span data-ttu-id="dee21-154">Password utente hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-154">Password for hello user.</span></span> |<span data-ttu-id="dee21-155">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="dee21-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="dee21-156">authSource</span><span class="sxs-lookup"><span data-stu-id="dee21-156">authSource</span></span> |<span data-ttu-id="dee21-157">Nome del database MongoDB hello che si desidera toouse toocheck le credenziali per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="dee21-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="dee21-158">Facoltativo (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="dee21-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="dee21-159">impostazione predefinita: Usa l'account amministratore hello e database hello specificato utilizzando la proprietà databaseName.</span><span class="sxs-lookup"><span data-stu-id="dee21-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="dee21-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="dee21-160">databaseName</span></span> |<span data-ttu-id="dee21-161">Nome del database MongoDB hello che si desidera tooaccess.</span><span class="sxs-lookup"><span data-stu-id="dee21-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="dee21-162">Sì</span><span class="sxs-lookup"><span data-stu-id="dee21-162">Yes</span></span> |
| <span data-ttu-id="dee21-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="dee21-163">gatewayName</span></span> |<span data-ttu-id="dee21-164">Nome del gateway hello che accede a hello archivio di dati.</span><span class="sxs-lookup"><span data-stu-id="dee21-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="dee21-165">Sì</span><span class="sxs-lookup"><span data-stu-id="dee21-165">Yes</span></span> |
| <span data-ttu-id="dee21-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="dee21-166">encryptedCredential</span></span> |<span data-ttu-id="dee21-167">Credenziali crittografate in base al gateway.</span><span class="sxs-lookup"><span data-stu-id="dee21-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="dee21-168">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="dee21-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="dee21-169">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="dee21-169">Dataset properties</span></span>
<span data-ttu-id="dee21-170">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="dee21-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="dee21-171">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="dee21-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="dee21-172">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="dee21-173">sezione Hello typeProperties per set di dati di tipo **MongoDbCollection** è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="dee21-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="dee21-174">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dee21-174">Property</span></span> | <span data-ttu-id="dee21-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dee21-175">Description</span></span> | <span data-ttu-id="dee21-176">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dee21-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dee21-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="dee21-177">collectionName</span></span> |<span data-ttu-id="dee21-178">Nome dell'insieme di hello nel database di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dee21-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="dee21-179">Sì</span><span class="sxs-lookup"><span data-stu-id="dee21-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="dee21-180">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="dee21-180">Copy activity properties</span></span>
<span data-ttu-id="dee21-181">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="dee21-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="dee21-182">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="dee21-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="dee21-183">Le proprietà disponibili nella hello **typeProperties** sezione di attività hello hello invece variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="dee21-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="dee21-184">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="dee21-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="dee21-185">Quando origine hello è di tipo **MongoDbSource** hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="dee21-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="dee21-186">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dee21-186">Property</span></span> | <span data-ttu-id="dee21-187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dee21-187">Description</span></span> | <span data-ttu-id="dee21-188">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="dee21-188">Allowed values</span></span> | <span data-ttu-id="dee21-189">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dee21-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dee21-190">query</span><span class="sxs-lookup"><span data-stu-id="dee21-190">query</span></span> |<span data-ttu-id="dee21-191">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="dee21-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="dee21-192">Stringa di query SQL-92.</span><span class="sxs-lookup"><span data-stu-id="dee21-192">SQL-92 query string.</span></span> <span data-ttu-id="dee21-193">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="dee21-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="dee21-194">No, se **collectionName** di **set di dati** è specificato</span><span class="sxs-lookup"><span data-stu-id="dee21-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="dee21-195">Esempio JSON: copiare i dati da tooAzure MongoDB Blob</span><span class="sxs-lookup"><span data-stu-id="dee21-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="dee21-196">In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dee21-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="dee21-197">Viene illustrato come toocopy dati da un tooan MongoDB locale archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="dee21-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="dee21-198">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dee21-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="dee21-199">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="dee21-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="dee21-200">Un servizio collegato di tipo [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dee21-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="dee21-201">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dee21-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="dee21-202">Un [set di dati](data-factory-create-datasets.md) di input di tipo [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dee21-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="dee21-203">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dee21-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="dee21-204">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [MongoDbSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dee21-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="dee21-205">esempio Hello copia dati da un risultato di query nell'oggetto blob tooa database MongoDB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="dee21-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="dee21-206">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="dee21-207">Come primo passaggio, configurare il gateway di gestione dati hello in base alle istruzioni hello hello [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="dee21-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="dee21-208">**Servizio collegato MongoDB:**</span><span class="sxs-lookup"><span data-stu-id="dee21-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="dee21-209">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="dee21-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="dee21-210">**Set di dati input MongoDB:** impostazione "external": "true" informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="dee21-211">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="dee21-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="dee21-212">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="dee21-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dee21-213">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="dee21-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="dee21-214">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="dee21-215">**Attività di copia in una pipeline con un'origine MongoDB e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="dee21-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="dee21-216">pipeline di Hello contiene un'attività di copia che è configurato toouse hello sopra i set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="dee21-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="dee21-217">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**MongoDbSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="dee21-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="dee21-218">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="dee21-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="dee21-219">Schema da Data Factory</span><span class="sxs-lookup"><span data-stu-id="dee21-219">Schema by Data Factory</span></span>
<span data-ttu-id="dee21-220">Servizio di Azure Data Factory deriva da una raccolta di MongoDB utilizzando documenti hello 100 più recente nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="dee21-221">Se questi 100 documenti non contengono completo dello schema, è possibile ignorare alcune colonne durante l'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="dee21-222">Mapping dei tipi per MongoDB</span><span class="sxs-lookup"><span data-stu-id="dee21-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="dee21-223">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="dee21-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="dee21-224">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="dee21-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="dee21-225">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="dee21-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="dee21-226">Durante lo spostamento di hello tooMongoDB dati seguenti vengono utilizzati i mapping dai tipi di MongoDB tipi too.NET.</span><span class="sxs-lookup"><span data-stu-id="dee21-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="dee21-227">Tipo di MongoDB</span><span class="sxs-lookup"><span data-stu-id="dee21-227">MongoDB type</span></span> | <span data-ttu-id="dee21-228">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dee21-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="dee21-229">Binary</span><span class="sxs-lookup"><span data-stu-id="dee21-229">Binary</span></span> |<span data-ttu-id="dee21-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="dee21-230">Byte[]</span></span> |
| <span data-ttu-id="dee21-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="dee21-231">Boolean</span></span> |<span data-ttu-id="dee21-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="dee21-232">Boolean</span></span> |
| <span data-ttu-id="dee21-233">Date</span><span class="sxs-lookup"><span data-stu-id="dee21-233">Date</span></span> |<span data-ttu-id="dee21-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="dee21-234">DateTime</span></span> |
| <span data-ttu-id="dee21-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="dee21-235">NumberDouble</span></span> |<span data-ttu-id="dee21-236">Double</span><span class="sxs-lookup"><span data-stu-id="dee21-236">Double</span></span> |
| <span data-ttu-id="dee21-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="dee21-237">NumberInt</span></span> |<span data-ttu-id="dee21-238">Int32</span><span class="sxs-lookup"><span data-stu-id="dee21-238">Int32</span></span> |
| <span data-ttu-id="dee21-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="dee21-239">NumberLong</span></span> |<span data-ttu-id="dee21-240">Int64</span><span class="sxs-lookup"><span data-stu-id="dee21-240">Int64</span></span> |
| <span data-ttu-id="dee21-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="dee21-241">ObjectID</span></span> |<span data-ttu-id="dee21-242">String</span><span class="sxs-lookup"><span data-stu-id="dee21-242">String</span></span> |
| <span data-ttu-id="dee21-243">String</span><span class="sxs-lookup"><span data-stu-id="dee21-243">String</span></span> |<span data-ttu-id="dee21-244">String</span><span class="sxs-lookup"><span data-stu-id="dee21-244">String</span></span> |
| <span data-ttu-id="dee21-245">UUID</span><span class="sxs-lookup"><span data-stu-id="dee21-245">UUID</span></span> |<span data-ttu-id="dee21-246">Guid</span><span class="sxs-lookup"><span data-stu-id="dee21-246">Guid</span></span> |
| <span data-ttu-id="dee21-247">Oggetto</span><span class="sxs-lookup"><span data-stu-id="dee21-247">Object</span></span> |<span data-ttu-id="dee21-248">Rinormalizzato in colonne rese flat con "_" come separatore annidato</span><span class="sxs-lookup"><span data-stu-id="dee21-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="dee21-249">toolearn sul supporto per le matrici con tabelle virtuali, vedere troppo[il supporto per i tipi complessi mediante tabelle virtuali](#support-for-complex-types-using-virtual-tables) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="dee21-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="dee21-250">Attualmente, non è supportato hello seguenti tipi di dati di MongoDB: DBPointer, JavaScript, minimo e massimo della chiave, espressioni regolari, simboli, Timestamp, non definito</span><span class="sxs-lookup"><span data-stu-id="dee21-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="dee21-251">Supporto per tipi complessi con tabelle virtuali</span><span class="sxs-lookup"><span data-stu-id="dee21-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="dee21-252">Data Factory di Azure Usa un ODBC driver tooconnect tooand copia dati predefinito del database MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dee21-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="dee21-253">Per i tipi complessi, ad esempio matrici o oggetti con tipi diversi in documenti hello, driver hello Normalizza nuovamente dati in tabelle virtuali corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="dee21-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="dee21-254">In particolare, se una tabella contiene colonne di tipo, il driver hello genera l'errore hello le tabelle virtuali seguenti:</span><span class="sxs-lookup"><span data-stu-id="dee21-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="dee21-255">Oggetto **tabella di base**, che contiene hello stessi dati di tabella ad eccezione delle colonne di tipo complesso hello hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="dee21-256">tabella di base Hello utilizza hello stesso nome come tabella reale hello che rappresenta.</span><span class="sxs-lookup"><span data-stu-id="dee21-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="dee21-257">Oggetto **tabella virtuale** per ogni colonna di tipo complesso, che espande dati hello annidato.</span><span class="sxs-lookup"><span data-stu-id="dee21-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="dee21-258">tabelle virtuali Hello vengono denominate usando il nome di hello della tabella reale hello, un separatore "_" e nome hello della matrice hello o un oggetto.</span><span class="sxs-lookup"><span data-stu-id="dee21-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="dee21-259">Tabelle virtuali fare riferimento ai dati toohello nella tabella reale hello, abilitazione hello driver tooaccess hello dati denormalizzati.</span><span class="sxs-lookup"><span data-stu-id="dee21-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="dee21-260">Per informazioni dettagliate, vedere la sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="dee21-260">See Example section below details.</span></span> <span data-ttu-id="dee21-261">È possibile accedere a contenuto hello di matrici di MongoDB eseguendo una query e join di tabelle virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="dee21-262">È possibile utilizzare hello [Copia guidata](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively visualizzazione elenco di tabelle nel database di MongoDB inclusi tabelle virtuali hello hello e visualizzare l'anteprima dati hello all'interno.</span><span class="sxs-lookup"><span data-stu-id="dee21-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="dee21-263">Inoltre, è possibile costruire una query nella copia guidata hello e convalidare i risultati di hello toosee.</span><span class="sxs-lookup"><span data-stu-id="dee21-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="dee21-264">Esempio</span><span class="sxs-lookup"><span data-stu-id="dee21-264">Example</span></span>
<span data-ttu-id="dee21-265">Ad esempio, "ExampleTable" di seguito è una tabella MongoDB che contiene una colonna con una matrice di oggetti in ogni cella (Fatture) e una colonna con una matrice di tipi scalari (Classificazioni).</span><span class="sxs-lookup"><span data-stu-id="dee21-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="dee21-266">_id</span><span class="sxs-lookup"><span data-stu-id="dee21-266">_id</span></span> | <span data-ttu-id="dee21-267">Nome del cliente</span><span class="sxs-lookup"><span data-stu-id="dee21-267">Customer Name</span></span> | <span data-ttu-id="dee21-268">Fatture</span><span class="sxs-lookup"><span data-stu-id="dee21-268">Invoices</span></span> | <span data-ttu-id="dee21-269">Contratto</span><span class="sxs-lookup"><span data-stu-id="dee21-269">Service Level</span></span> | <span data-ttu-id="dee21-270">Classificazioni</span><span class="sxs-lookup"><span data-stu-id="dee21-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="dee21-271">1111</span><span class="sxs-lookup"><span data-stu-id="dee21-271">1111</span></span> |<span data-ttu-id="dee21-272">ABC</span><span class="sxs-lookup"><span data-stu-id="dee21-272">ABC</span></span> |<span data-ttu-id="dee21-273">[{invoice_id:"123", item:"toaster", price:"456", discount:"0.2"}, {invoice_id:"124", item:"oven", price: "1235", discount: "0.2"}]</span><span class="sxs-lookup"><span data-stu-id="dee21-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="dee21-274">Silver</span><span class="sxs-lookup"><span data-stu-id="dee21-274">Silver</span></span> |<span data-ttu-id="dee21-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="dee21-275">[5,6]</span></span> |
| <span data-ttu-id="dee21-276">2222</span><span class="sxs-lookup"><span data-stu-id="dee21-276">2222</span></span> |<span data-ttu-id="dee21-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="dee21-277">XYZ</span></span> |<span data-ttu-id="dee21-278">[{invoice_id:"135", item:"fridge", price: "12543", discount: "0.0"}]</span><span class="sxs-lookup"><span data-stu-id="dee21-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="dee21-279">Gold</span><span class="sxs-lookup"><span data-stu-id="dee21-279">Gold</span></span> |<span data-ttu-id="dee21-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="dee21-280">[1,2]</span></span> |

<span data-ttu-id="dee21-281">driver Hello genera più tabelle virtuali toorepresent di questa tabella.</span><span class="sxs-lookup"><span data-stu-id="dee21-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="dee21-282">Hello prima virtuale è hello base tabella denominata "ExampleTable", illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="dee21-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="dee21-283">tabella di base Hello contiene tutti i dati della tabella originale hello hello, ma i dati di hello da matrici di hello sono stato omesso e viene espanso nella tabelle virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="dee21-284">_id</span><span class="sxs-lookup"><span data-stu-id="dee21-284">_id</span></span> | <span data-ttu-id="dee21-285">Nome del cliente</span><span class="sxs-lookup"><span data-stu-id="dee21-285">Customer Name</span></span> | <span data-ttu-id="dee21-286">Contratto</span><span class="sxs-lookup"><span data-stu-id="dee21-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dee21-287">1111</span><span class="sxs-lookup"><span data-stu-id="dee21-287">1111</span></span> |<span data-ttu-id="dee21-288">ABC</span><span class="sxs-lookup"><span data-stu-id="dee21-288">ABC</span></span> |<span data-ttu-id="dee21-289">Silver</span><span class="sxs-lookup"><span data-stu-id="dee21-289">Silver</span></span> |
| <span data-ttu-id="dee21-290">2222</span><span class="sxs-lookup"><span data-stu-id="dee21-290">2222</span></span> |<span data-ttu-id="dee21-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="dee21-291">XYZ</span></span> |<span data-ttu-id="dee21-292">Gold</span><span class="sxs-lookup"><span data-stu-id="dee21-292">Gold</span></span> |

<span data-ttu-id="dee21-293">Hello tabelle seguenti illustrano hello tabelle virtuali che rappresentano matrici originale di hello nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="dee21-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="dee21-294">Queste tabelle contengono seguente hello:</span><span class="sxs-lookup"><span data-stu-id="dee21-294">These tables contain hello following:</span></span>

* <span data-ttu-id="dee21-295">Un riferimento toohello colonna chiave primaria corrispondente toohello riga originale della matrice originale hello (tramite colonna ID hello)</span><span class="sxs-lookup"><span data-stu-id="dee21-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="dee21-296">Indicazione della posizione di hello dei dati di hello all'interno della matrice originale hello</span><span class="sxs-lookup"><span data-stu-id="dee21-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="dee21-297">Hello espanso dati per ogni elemento all'interno della matrice hello</span><span class="sxs-lookup"><span data-stu-id="dee21-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="dee21-298">Tabella "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="dee21-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="dee21-299">_id</span><span class="sxs-lookup"><span data-stu-id="dee21-299">_id</span></span> | <span data-ttu-id="dee21-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="dee21-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="dee21-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="dee21-301">invoice_id</span></span> | <span data-ttu-id="dee21-302">item</span><span class="sxs-lookup"><span data-stu-id="dee21-302">item</span></span> | <span data-ttu-id="dee21-303">price</span><span class="sxs-lookup"><span data-stu-id="dee21-303">price</span></span> | <span data-ttu-id="dee21-304">Discount</span><span class="sxs-lookup"><span data-stu-id="dee21-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="dee21-305">1111</span><span class="sxs-lookup"><span data-stu-id="dee21-305">1111</span></span> |<span data-ttu-id="dee21-306">0</span><span class="sxs-lookup"><span data-stu-id="dee21-306">0</span></span> |<span data-ttu-id="dee21-307">123</span><span class="sxs-lookup"><span data-stu-id="dee21-307">123</span></span> |<span data-ttu-id="dee21-308">toaster</span><span class="sxs-lookup"><span data-stu-id="dee21-308">toaster</span></span> |<span data-ttu-id="dee21-309">456</span><span class="sxs-lookup"><span data-stu-id="dee21-309">456</span></span> |<span data-ttu-id="dee21-310">0,2</span><span class="sxs-lookup"><span data-stu-id="dee21-310">0.2</span></span> |
| <span data-ttu-id="dee21-311">1111</span><span class="sxs-lookup"><span data-stu-id="dee21-311">1111</span></span> |<span data-ttu-id="dee21-312">1</span><span class="sxs-lookup"><span data-stu-id="dee21-312">1</span></span> |<span data-ttu-id="dee21-313">124</span><span class="sxs-lookup"><span data-stu-id="dee21-313">124</span></span> |<span data-ttu-id="dee21-314">oven</span><span class="sxs-lookup"><span data-stu-id="dee21-314">oven</span></span> |<span data-ttu-id="dee21-315">1235</span><span class="sxs-lookup"><span data-stu-id="dee21-315">1235</span></span> |<span data-ttu-id="dee21-316">0,2</span><span class="sxs-lookup"><span data-stu-id="dee21-316">0.2</span></span> |
| <span data-ttu-id="dee21-317">2222</span><span class="sxs-lookup"><span data-stu-id="dee21-317">2222</span></span> |<span data-ttu-id="dee21-318">0</span><span class="sxs-lookup"><span data-stu-id="dee21-318">0</span></span> |<span data-ttu-id="dee21-319">135</span><span class="sxs-lookup"><span data-stu-id="dee21-319">135</span></span> |<span data-ttu-id="dee21-320">fridge</span><span class="sxs-lookup"><span data-stu-id="dee21-320">fridge</span></span> |<span data-ttu-id="dee21-321">12543</span><span class="sxs-lookup"><span data-stu-id="dee21-321">12543</span></span> |<span data-ttu-id="dee21-322">0.0</span><span class="sxs-lookup"><span data-stu-id="dee21-322">0.0</span></span> |

<span data-ttu-id="dee21-323">Tabella "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="dee21-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="dee21-324">_id</span><span class="sxs-lookup"><span data-stu-id="dee21-324">_id</span></span> | <span data-ttu-id="dee21-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="dee21-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="dee21-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="dee21-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dee21-327">1111</span><span class="sxs-lookup"><span data-stu-id="dee21-327">1111</span></span> |<span data-ttu-id="dee21-328">0</span><span class="sxs-lookup"><span data-stu-id="dee21-328">0</span></span> |<span data-ttu-id="dee21-329">5</span><span class="sxs-lookup"><span data-stu-id="dee21-329">5</span></span> |
| <span data-ttu-id="dee21-330">1111</span><span class="sxs-lookup"><span data-stu-id="dee21-330">1111</span></span> |<span data-ttu-id="dee21-331">1</span><span class="sxs-lookup"><span data-stu-id="dee21-331">1</span></span> |<span data-ttu-id="dee21-332">6</span><span class="sxs-lookup"><span data-stu-id="dee21-332">6</span></span> |
| <span data-ttu-id="dee21-333">2222</span><span class="sxs-lookup"><span data-stu-id="dee21-333">2222</span></span> |<span data-ttu-id="dee21-334">0</span><span class="sxs-lookup"><span data-stu-id="dee21-334">0</span></span> |<span data-ttu-id="dee21-335">1</span><span class="sxs-lookup"><span data-stu-id="dee21-335">1</span></span> |
| <span data-ttu-id="dee21-336">2222</span><span class="sxs-lookup"><span data-stu-id="dee21-336">2222</span></span> |<span data-ttu-id="dee21-337">1</span><span class="sxs-lookup"><span data-stu-id="dee21-337">1</span></span> |<span data-ttu-id="dee21-338">2</span><span class="sxs-lookup"><span data-stu-id="dee21-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="dee21-339">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="dee21-339">Map source toosink columns</span></span>
<span data-ttu-id="dee21-340">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="dee21-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="dee21-341">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="dee21-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="dee21-342">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="dee21-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="dee21-343">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="dee21-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="dee21-344">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="dee21-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="dee21-345">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="dee21-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="dee21-346">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="dee21-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="dee21-347">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="dee21-347">Performance and Tuning</span></span>
<span data-ttu-id="dee21-348">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="dee21-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dee21-349">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dee21-349">Next Steps</span></span>
<span data-ttu-id="dee21-350">Vedere [spostare i dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo per istruzioni dettagliate per la creazione di una pipeline di dati che consente di spostare dati da un locale tooan archiviano dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="dee21-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
