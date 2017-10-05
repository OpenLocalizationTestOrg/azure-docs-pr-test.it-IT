---
title: Spostare dati da MongoDB con Data Factory | Documentazione Microsoft
description: Informazioni su come spostare i dati dal database di MongoDB con Azure Data Factory.
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
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="d5ef1-103">Spostare i dati da MongoDB con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ef1-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="d5ef1-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un database MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="d5ef1-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="d5ef1-106">È possibile copiare dati da un archivio dati MongoDB locale a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="d5ef1-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d5ef1-108">Data Factory supporta attualmente solo lo spostamento dei dati da un archivio dati MongoDB ad altri archivi dati, ma non da altri archivi dati a un archivio dati MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d5ef1-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5ef1-109">Prerequisites</span></span>
<span data-ttu-id="d5ef1-110">Per consentire al servizio Azure Data Factory di connettersi al database MongoDB in locale, è necessario installare i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="d5ef1-111">Le versioni MongoDB supportate sono 2.4, 2.6, 3.0 e 3.2.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="d5ef1-112">Gateway di gestione dati nello stesso computer che ospita il database o in un computer separato per evitare che competa per le risorse con il database.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="d5ef1-113">Il Gateway di gestione dati è un software che connette le origini dati locali ai servizi cloud in modo sicuro e gestito.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="d5ef1-114">Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="d5ef1-115">Per istruzioni passo per passo su come configurare il gateway di una pipeline di dati per spostare i dati, vedere [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="d5ef1-116">Quando si installa il gateway, viene installato automaticamente un driver ODBC MongoDB Microsoft che viene usato per la connessione a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5ef1-117">È necessario usare il gateway per connettersi a MongoDB anche se è ospitato in VM IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="d5ef1-118">Se si sta provando a connettersi a un'istanza di MongoDB ospitata nel cloud è anche possibile installare l'istanza del gateway nella macchina virtuale IaaS.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d5ef1-119">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d5ef1-119">Getting started</span></span>
<span data-ttu-id="d5ef1-120">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un archivio dati MongoDB usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="d5ef1-121">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d5ef1-122">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d5ef1-123">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d5ef1-124">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d5ef1-125">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="d5ef1-126">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d5ef1-127">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="d5ef1-128">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d5ef1-129">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d5ef1-130">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d5ef1-131">Per un esempio con definizioni JSON per entità di data factory utilizzate per copiare dati da un archivio dati MongoDB locale, vedere la sezione [Esempio JSON: Copiare dati da MongoDB al BLOB di Azure](#json-example-copy-data-from-mongodb-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d5ef1-132">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche dell'origine MongoDB:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d5ef1-133">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="d5ef1-133">Linked service properties</span></span>
<span data-ttu-id="d5ef1-134">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato **OnPremisesMongoDB** .</span><span class="sxs-lookup"><span data-stu-id="d5ef1-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="d5ef1-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d5ef1-135">Property</span></span> | <span data-ttu-id="d5ef1-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5ef1-136">Description</span></span> | <span data-ttu-id="d5ef1-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d5ef1-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5ef1-138">type</span><span class="sxs-lookup"><span data-stu-id="d5ef1-138">type</span></span> |<span data-ttu-id="d5ef1-139">La proprietà type deve essere impostata su: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="d5ef1-140">Sì</span><span class="sxs-lookup"><span data-stu-id="d5ef1-140">Yes</span></span> |
| <span data-ttu-id="d5ef1-141">server</span><span class="sxs-lookup"><span data-stu-id="d5ef1-141">server</span></span> |<span data-ttu-id="d5ef1-142">Indirizzo IP o nome host del server MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="d5ef1-143">Sì</span><span class="sxs-lookup"><span data-stu-id="d5ef1-143">Yes</span></span> |
| <span data-ttu-id="d5ef1-144">port</span><span class="sxs-lookup"><span data-stu-id="d5ef1-144">port</span></span> |<span data-ttu-id="d5ef1-145">Porta TCP che il server MongoDB usa per ascoltare le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="d5ef1-146">Facoltativo, valore predefinito: 27017</span><span class="sxs-lookup"><span data-stu-id="d5ef1-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="d5ef1-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d5ef1-147">authenticationType</span></span> |<span data-ttu-id="d5ef1-148">Di base o anonima.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="d5ef1-149">Sì</span><span class="sxs-lookup"><span data-stu-id="d5ef1-149">Yes</span></span> |
| <span data-ttu-id="d5ef1-150">username</span><span class="sxs-lookup"><span data-stu-id="d5ef1-150">username</span></span> |<span data-ttu-id="d5ef1-151">Account utente per accedere a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-151">User account to access MongoDB.</span></span> |<span data-ttu-id="d5ef1-152">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="d5ef1-153">password</span><span class="sxs-lookup"><span data-stu-id="d5ef1-153">password</span></span> |<span data-ttu-id="d5ef1-154">Password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-154">Password for the user.</span></span> |<span data-ttu-id="d5ef1-155">Sì (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="d5ef1-156">authSource</span><span class="sxs-lookup"><span data-stu-id="d5ef1-156">authSource</span></span> |<span data-ttu-id="d5ef1-157">Nome del database MongoDB che si vuole usare per controllare le credenziali di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="d5ef1-158">Facoltativo (se si usa l'autenticazione di base).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="d5ef1-159">Predefinito: usa l'account di amministrazione e il database specificato usando la proprietà databaseName.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="d5ef1-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="d5ef1-160">databaseName</span></span> |<span data-ttu-id="d5ef1-161">Nome del database MongoDB a cui si vuole accedere.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="d5ef1-162">Sì</span><span class="sxs-lookup"><span data-stu-id="d5ef1-162">Yes</span></span> |
| <span data-ttu-id="d5ef1-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d5ef1-163">gatewayName</span></span> |<span data-ttu-id="d5ef1-164">Nome del gateway che accede all'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="d5ef1-165">Sì</span><span class="sxs-lookup"><span data-stu-id="d5ef1-165">Yes</span></span> |
| <span data-ttu-id="d5ef1-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d5ef1-166">encryptedCredential</span></span> |<span data-ttu-id="d5ef1-167">Credenziali crittografate in base al gateway.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="d5ef1-168">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="d5ef1-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="d5ef1-169">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="d5ef1-169">Dataset properties</span></span>
<span data-ttu-id="d5ef1-170">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d5ef1-171">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d5ef1-172">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d5ef1-173">La sezione typeProperties per il set di dati di tipo **MongoDbCollection** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="d5ef1-174">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d5ef1-174">Property</span></span> | <span data-ttu-id="d5ef1-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5ef1-175">Description</span></span> | <span data-ttu-id="d5ef1-176">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d5ef1-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5ef1-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="d5ef1-177">collectionName</span></span> |<span data-ttu-id="d5ef1-178">Nome della raccolta nel database MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="d5ef1-179">Sì</span><span class="sxs-lookup"><span data-stu-id="d5ef1-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d5ef1-180">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="d5ef1-180">Copy activity properties</span></span>
<span data-ttu-id="d5ef1-181">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d5ef1-182">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="d5ef1-183">D'altra parte, le proprietà disponibili nella sezione **typeProperties** dell'attività variano in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="d5ef1-184">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d5ef1-185">In caso di origine di tipo **MongoDbSource** , nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d5ef1-186">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d5ef1-186">Property</span></span> | <span data-ttu-id="d5ef1-187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5ef1-187">Description</span></span> | <span data-ttu-id="d5ef1-188">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d5ef1-188">Allowed values</span></span> | <span data-ttu-id="d5ef1-189">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d5ef1-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ef1-190">query</span><span class="sxs-lookup"><span data-stu-id="d5ef1-190">query</span></span> |<span data-ttu-id="d5ef1-191">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-191">Use the custom query to read data.</span></span> |<span data-ttu-id="d5ef1-192">Stringa di query SQL-92.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-192">SQL-92 query string.</span></span> <span data-ttu-id="d5ef1-193">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="d5ef1-194">No, se **collectionName** di **set di dati** è specificato</span><span class="sxs-lookup"><span data-stu-id="d5ef1-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="d5ef1-195">Esempio JSON: Copiare dati da MongoDB al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d5ef1-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="d5ef1-196">Questo esempio fornisce le definizioni JSON di esempio da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d5ef1-197">Illustra come copiare dati da un MongoDB locale a un'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="d5ef1-198">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="d5ef1-199">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="d5ef1-200">Un servizio collegato di tipo [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="d5ef1-201">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d5ef1-202">Un [set di dati](data-factory-create-datasets.md) di input di tipo [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="d5ef1-203">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d5ef1-204">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [MongoDbSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d5ef1-205">L'esempio copia i dati dai risultati della query nel database MongoDB in un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="d5ef1-206">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d5ef1-207">Per prima cosa, impostare il Gateway di gestione dati in base alle istruzioni contenute nell'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) .</span><span class="sxs-lookup"><span data-stu-id="d5ef1-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="d5ef1-208">**Servizio collegato MongoDB:**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="d5ef1-209">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="d5ef1-210">**Set di dati di input MongoDB:** impostando "external": "true" si comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="d5ef1-211">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d5ef1-212">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d5ef1-213">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d5ef1-214">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="d5ef1-215">**Attività di copia in una pipeline con un'origine MongoDB e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="d5ef1-216">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output precedenti. È programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d5ef1-217">Nella definizione JSON della pipeline, il tipo **source** è impostato su **MongoDbSource** e il tipo **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d5ef1-218">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="d5ef1-219">Schema da Data Factory</span><span class="sxs-lookup"><span data-stu-id="d5ef1-219">Schema by Data Factory</span></span>
<span data-ttu-id="d5ef1-220">Il servizio Azure Data Factory deduce lo schema da una raccolta MongoDB usando gli ultimi 100 documenti nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="d5ef1-221">Se questi 100 documenti non contengono lo schema completo, alcune colonne possono essere ignorate durante l'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="d5ef1-222">Mapping dei tipi per MongoDB</span><span class="sxs-lookup"><span data-stu-id="d5ef1-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="d5ef1-223">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="d5ef1-224">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d5ef1-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d5ef1-225">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="d5ef1-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d5ef1-226">Quando si spostano i dati in MongoDB vengono usati i mapping seguenti dai tipi MongoDB ai tipi .NET.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="d5ef1-227">Tipo di MongoDB</span><span class="sxs-lookup"><span data-stu-id="d5ef1-227">MongoDB type</span></span> | <span data-ttu-id="d5ef1-228">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d5ef1-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="d5ef1-229">Binary</span><span class="sxs-lookup"><span data-stu-id="d5ef1-229">Binary</span></span> |<span data-ttu-id="d5ef1-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d5ef1-230">Byte[]</span></span> |
| <span data-ttu-id="d5ef1-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="d5ef1-231">Boolean</span></span> |<span data-ttu-id="d5ef1-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="d5ef1-232">Boolean</span></span> |
| <span data-ttu-id="d5ef1-233">Date</span><span class="sxs-lookup"><span data-stu-id="d5ef1-233">Date</span></span> |<span data-ttu-id="d5ef1-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="d5ef1-234">DateTime</span></span> |
| <span data-ttu-id="d5ef1-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="d5ef1-235">NumberDouble</span></span> |<span data-ttu-id="d5ef1-236">Double</span><span class="sxs-lookup"><span data-stu-id="d5ef1-236">Double</span></span> |
| <span data-ttu-id="d5ef1-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="d5ef1-237">NumberInt</span></span> |<span data-ttu-id="d5ef1-238">Int32</span><span class="sxs-lookup"><span data-stu-id="d5ef1-238">Int32</span></span> |
| <span data-ttu-id="d5ef1-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="d5ef1-239">NumberLong</span></span> |<span data-ttu-id="d5ef1-240">Int64</span><span class="sxs-lookup"><span data-stu-id="d5ef1-240">Int64</span></span> |
| <span data-ttu-id="d5ef1-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="d5ef1-241">ObjectID</span></span> |<span data-ttu-id="d5ef1-242">String</span><span class="sxs-lookup"><span data-stu-id="d5ef1-242">String</span></span> |
| <span data-ttu-id="d5ef1-243">String</span><span class="sxs-lookup"><span data-stu-id="d5ef1-243">String</span></span> |<span data-ttu-id="d5ef1-244">String</span><span class="sxs-lookup"><span data-stu-id="d5ef1-244">String</span></span> |
| <span data-ttu-id="d5ef1-245">UUID</span><span class="sxs-lookup"><span data-stu-id="d5ef1-245">UUID</span></span> |<span data-ttu-id="d5ef1-246">Guid</span><span class="sxs-lookup"><span data-stu-id="d5ef1-246">Guid</span></span> |
| <span data-ttu-id="d5ef1-247">Oggetto</span><span class="sxs-lookup"><span data-stu-id="d5ef1-247">Object</span></span> |<span data-ttu-id="d5ef1-248">Rinormalizzato in colonne rese flat con "_" come separatore annidato</span><span class="sxs-lookup"><span data-stu-id="d5ef1-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="d5ef1-249">Per informazioni sul supporto di matrici che usano tabelle virtuali, vedere la sezione [Supporto per tipi complessi con tabelle virtuali](#support-for-complex-types-using-virtual-tables) qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="d5ef1-250">I tipi di dati MongoDB seguenti non sono attualmente supportati: DBPointer, JavaScript, chiave Max/Min, Espressione regolare, Simbolo, Timestamp, Undefined</span><span class="sxs-lookup"><span data-stu-id="d5ef1-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="d5ef1-251">Supporto per tipi complessi con tabelle virtuali</span><span class="sxs-lookup"><span data-stu-id="d5ef1-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="d5ef1-252">Azure Data Factory usa un driver ODBC integrato per connettersi ai dati di un database MongoDB e copiarli.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="d5ef1-253">Per i tipi complessi come le matrici o gli oggetti con tipi diversi tra i documenti, il driver rinormalizza i dati nelle tabelle virtuali corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="d5ef1-254">In particolare, se una tabella contiene tali colonne, il driver genera le tabelle virtuali seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="d5ef1-255">Una **tabella di base**che contiene gli stessi dati della tabella reale eccetto le colonne di tipo complesso.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="d5ef1-256">La tabella di base ha lo stesso nome della tabella reale che rappresenta.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="d5ef1-257">Una **tabella virtuale** per ogni colonna di tipo complesso che espande i dati annidati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="d5ef1-258">Alle tabelle virtuali vengono assegnati nomi composti dal nome della tabella reale seguito dal separatore "_" e dal nome della matrice o dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="d5ef1-259">Le tabelle virtuali fanno riferimento ai dati nella tabella reale, consentendo al driver di accedere ai dati denormalizzati.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="d5ef1-260">Per informazioni dettagliate, vedere la sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-260">See Example section below details.</span></span> <span data-ttu-id="d5ef1-261">È possibile accedere al contenuto delle matrici MongoDB eseguendo query e join sulle tabelle virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="d5ef1-262">È possibile usare la [Copia guidata](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) per visualizzare intuitivamente l'elenco delle tabelle nel database MongoDB che includono tabelle virtuali e visualizzare in anteprima i dati all'interno.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="d5ef1-263">È inoltre possibile costruire una query nella Copia guidata ed eseguire la convalida per visualizzare il risultato.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="d5ef1-264">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5ef1-264">Example</span></span>
<span data-ttu-id="d5ef1-265">Ad esempio, "ExampleTable" di seguito è una tabella MongoDB che contiene una colonna con una matrice di oggetti in ogni cella (Fatture) e una colonna con una matrice di tipi scalari (Classificazioni).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="d5ef1-266">_id</span><span class="sxs-lookup"><span data-stu-id="d5ef1-266">_id</span></span> | <span data-ttu-id="d5ef1-267">Nome del cliente</span><span class="sxs-lookup"><span data-stu-id="d5ef1-267">Customer Name</span></span> | <span data-ttu-id="d5ef1-268">Fatture</span><span class="sxs-lookup"><span data-stu-id="d5ef1-268">Invoices</span></span> | <span data-ttu-id="d5ef1-269">Contratto</span><span class="sxs-lookup"><span data-stu-id="d5ef1-269">Service Level</span></span> | <span data-ttu-id="d5ef1-270">Classificazioni</span><span class="sxs-lookup"><span data-stu-id="d5ef1-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d5ef1-271">1111</span><span class="sxs-lookup"><span data-stu-id="d5ef1-271">1111</span></span> |<span data-ttu-id="d5ef1-272">ABC</span><span class="sxs-lookup"><span data-stu-id="d5ef1-272">ABC</span></span> |<span data-ttu-id="d5ef1-273">[{invoice_id:"123", item:"toaster", price:"456", discount:"0.2"}, {invoice_id:"124", item:"oven", price: "1235", discount: "0.2"}]</span><span class="sxs-lookup"><span data-stu-id="d5ef1-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="d5ef1-274">Silver</span><span class="sxs-lookup"><span data-stu-id="d5ef1-274">Silver</span></span> |<span data-ttu-id="d5ef1-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="d5ef1-275">[5,6]</span></span> |
| <span data-ttu-id="d5ef1-276">2222</span><span class="sxs-lookup"><span data-stu-id="d5ef1-276">2222</span></span> |<span data-ttu-id="d5ef1-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="d5ef1-277">XYZ</span></span> |<span data-ttu-id="d5ef1-278">[{invoice_id:"135", item:"fridge", price: "12543", discount: "0.0"}]</span><span class="sxs-lookup"><span data-stu-id="d5ef1-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="d5ef1-279">Gold</span><span class="sxs-lookup"><span data-stu-id="d5ef1-279">Gold</span></span> |<span data-ttu-id="d5ef1-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="d5ef1-280">[1,2]</span></span> |

<span data-ttu-id="d5ef1-281">Il driver genera più tabelle virtuali per rappresentare questa singola tabella.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="d5ef1-282">La prima tabella virtuale è la tabella di base denominata "ExampleTable", illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="d5ef1-283">La tabella di base contiene tutti i dati della tabella originale, ma i dati dalle matrici sono stati omessi e vengono espansi nelle tabelle virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="d5ef1-284">_id</span><span class="sxs-lookup"><span data-stu-id="d5ef1-284">_id</span></span> | <span data-ttu-id="d5ef1-285">Nome del cliente</span><span class="sxs-lookup"><span data-stu-id="d5ef1-285">Customer Name</span></span> | <span data-ttu-id="d5ef1-286">Contratto</span><span class="sxs-lookup"><span data-stu-id="d5ef1-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5ef1-287">1111</span><span class="sxs-lookup"><span data-stu-id="d5ef1-287">1111</span></span> |<span data-ttu-id="d5ef1-288">ABC</span><span class="sxs-lookup"><span data-stu-id="d5ef1-288">ABC</span></span> |<span data-ttu-id="d5ef1-289">Silver</span><span class="sxs-lookup"><span data-stu-id="d5ef1-289">Silver</span></span> |
| <span data-ttu-id="d5ef1-290">2222</span><span class="sxs-lookup"><span data-stu-id="d5ef1-290">2222</span></span> |<span data-ttu-id="d5ef1-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="d5ef1-291">XYZ</span></span> |<span data-ttu-id="d5ef1-292">Gold</span><span class="sxs-lookup"><span data-stu-id="d5ef1-292">Gold</span></span> |

<span data-ttu-id="d5ef1-293">Le tabelle seguenti illustrano le tabelle virtuali che rappresentano le matrici originali nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="d5ef1-294">In queste tabelle è possibile vedere:</span><span class="sxs-lookup"><span data-stu-id="d5ef1-294">These tables contain the following:</span></span>

* <span data-ttu-id="d5ef1-295">Un riferimento alla colonna della chiave primaria originale corrispondente alla riga della matrice originale (con la colonna _id)</span><span class="sxs-lookup"><span data-stu-id="d5ef1-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="d5ef1-296">Un'indicazione della posizione dei dati all'interno della matrice originale</span><span class="sxs-lookup"><span data-stu-id="d5ef1-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="d5ef1-297">I dati espansi per ogni elemento all'interno della matrice</span><span class="sxs-lookup"><span data-stu-id="d5ef1-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="d5ef1-298">Tabella "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="d5ef1-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="d5ef1-299">_id</span><span class="sxs-lookup"><span data-stu-id="d5ef1-299">_id</span></span> | <span data-ttu-id="d5ef1-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="d5ef1-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="d5ef1-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="d5ef1-301">invoice_id</span></span> | <span data-ttu-id="d5ef1-302">item</span><span class="sxs-lookup"><span data-stu-id="d5ef1-302">item</span></span> | <span data-ttu-id="d5ef1-303">price</span><span class="sxs-lookup"><span data-stu-id="d5ef1-303">price</span></span> | <span data-ttu-id="d5ef1-304">Discount</span><span class="sxs-lookup"><span data-stu-id="d5ef1-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d5ef1-305">1111</span><span class="sxs-lookup"><span data-stu-id="d5ef1-305">1111</span></span> |<span data-ttu-id="d5ef1-306">0</span><span class="sxs-lookup"><span data-stu-id="d5ef1-306">0</span></span> |<span data-ttu-id="d5ef1-307">123</span><span class="sxs-lookup"><span data-stu-id="d5ef1-307">123</span></span> |<span data-ttu-id="d5ef1-308">toaster</span><span class="sxs-lookup"><span data-stu-id="d5ef1-308">toaster</span></span> |<span data-ttu-id="d5ef1-309">456</span><span class="sxs-lookup"><span data-stu-id="d5ef1-309">456</span></span> |<span data-ttu-id="d5ef1-310">0,2</span><span class="sxs-lookup"><span data-stu-id="d5ef1-310">0.2</span></span> |
| <span data-ttu-id="d5ef1-311">1111</span><span class="sxs-lookup"><span data-stu-id="d5ef1-311">1111</span></span> |<span data-ttu-id="d5ef1-312">1</span><span class="sxs-lookup"><span data-stu-id="d5ef1-312">1</span></span> |<span data-ttu-id="d5ef1-313">124</span><span class="sxs-lookup"><span data-stu-id="d5ef1-313">124</span></span> |<span data-ttu-id="d5ef1-314">oven</span><span class="sxs-lookup"><span data-stu-id="d5ef1-314">oven</span></span> |<span data-ttu-id="d5ef1-315">1235</span><span class="sxs-lookup"><span data-stu-id="d5ef1-315">1235</span></span> |<span data-ttu-id="d5ef1-316">0,2</span><span class="sxs-lookup"><span data-stu-id="d5ef1-316">0.2</span></span> |
| <span data-ttu-id="d5ef1-317">2222</span><span class="sxs-lookup"><span data-stu-id="d5ef1-317">2222</span></span> |<span data-ttu-id="d5ef1-318">0</span><span class="sxs-lookup"><span data-stu-id="d5ef1-318">0</span></span> |<span data-ttu-id="d5ef1-319">135</span><span class="sxs-lookup"><span data-stu-id="d5ef1-319">135</span></span> |<span data-ttu-id="d5ef1-320">fridge</span><span class="sxs-lookup"><span data-stu-id="d5ef1-320">fridge</span></span> |<span data-ttu-id="d5ef1-321">12543</span><span class="sxs-lookup"><span data-stu-id="d5ef1-321">12543</span></span> |<span data-ttu-id="d5ef1-322">0.0</span><span class="sxs-lookup"><span data-stu-id="d5ef1-322">0.0</span></span> |

<span data-ttu-id="d5ef1-323">Tabella "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="d5ef1-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="d5ef1-324">_id</span><span class="sxs-lookup"><span data-stu-id="d5ef1-324">_id</span></span> | <span data-ttu-id="d5ef1-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="d5ef1-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="d5ef1-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="d5ef1-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5ef1-327">1111</span><span class="sxs-lookup"><span data-stu-id="d5ef1-327">1111</span></span> |<span data-ttu-id="d5ef1-328">0</span><span class="sxs-lookup"><span data-stu-id="d5ef1-328">0</span></span> |<span data-ttu-id="d5ef1-329">5</span><span class="sxs-lookup"><span data-stu-id="d5ef1-329">5</span></span> |
| <span data-ttu-id="d5ef1-330">1111</span><span class="sxs-lookup"><span data-stu-id="d5ef1-330">1111</span></span> |<span data-ttu-id="d5ef1-331">1</span><span class="sxs-lookup"><span data-stu-id="d5ef1-331">1</span></span> |<span data-ttu-id="d5ef1-332">6</span><span class="sxs-lookup"><span data-stu-id="d5ef1-332">6</span></span> |
| <span data-ttu-id="d5ef1-333">2222</span><span class="sxs-lookup"><span data-stu-id="d5ef1-333">2222</span></span> |<span data-ttu-id="d5ef1-334">0</span><span class="sxs-lookup"><span data-stu-id="d5ef1-334">0</span></span> |<span data-ttu-id="d5ef1-335">1</span><span class="sxs-lookup"><span data-stu-id="d5ef1-335">1</span></span> |
| <span data-ttu-id="d5ef1-336">2222</span><span class="sxs-lookup"><span data-stu-id="d5ef1-336">2222</span></span> |<span data-ttu-id="d5ef1-337">1</span><span class="sxs-lookup"><span data-stu-id="d5ef1-337">1</span></span> |<span data-ttu-id="d5ef1-338">2</span><span class="sxs-lookup"><span data-stu-id="d5ef1-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d5ef1-339">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="d5ef1-339">Map source to sink columns</span></span>
<span data-ttu-id="d5ef1-340">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d5ef1-341">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="d5ef1-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="d5ef1-342">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d5ef1-343">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d5ef1-344">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d5ef1-345">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d5ef1-346">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d5ef1-347">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d5ef1-347">Performance and Tuning</span></span>
<span data-ttu-id="d5ef1-348">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5ef1-349">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5ef1-349">Next Steps</span></span>
<span data-ttu-id="d5ef1-350">Vedere l'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate sulla creazione di una pipeline di dati che sposta i dati da un archivio dati locale a un archivio dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
