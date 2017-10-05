---
title: Spostare dati da PostgreSQL usando Azure Data Factory | Documentazione Microsoft
description: Informazioni su come spostare i dati dal database di PostgreSQL mediante Data factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: fd26f0d03f8b0b352a6544a81ad952d2e2a1b7a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="8406c-103">Spostare i dati da PostgreSQL mediante Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="8406c-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="8406c-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare dati da un database PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="8406c-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="8406c-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="8406c-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="8406c-106">È possibile copiare dati da un archivio dati PostgreSQL locale a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="8406c-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="8406c-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8406c-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="8406c-108">Data Factory supporta attualmente lo spostamento di dati da un database PostgreSQL ad altri archivi dati, ma non da altri archivi dati a un database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-108">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8406c-109">prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8406c-109">prerequisites</span></span>

<span data-ttu-id="8406c-110">Data factory supporta la connessione a origini PostgreSQL locali tramite il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="8406c-111">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="8406c-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="8406c-112">Il gateway è necessario anche se il database PostgreSQL è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="8406c-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="8406c-113">È possibile installare il gateway nella stessa macchina virtuale IaaS dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="8406c-113">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="8406c-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="8406c-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="8406c-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="8406c-115">Supported versions and installation</span></span>
<span data-ttu-id="8406c-116">Perché Gateway di gestione dati si connetta al database PostgreSQL, installare il [provider di dati Ngpsql per PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 o versione successiva nello stesso sistema di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-116">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="8406c-117">Sono supportate le versioni di PostgreSQL a partire dalla 7.4.</span><span class="sxs-lookup"><span data-stu-id="8406c-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8406c-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="8406c-118">Getting started</span></span>
<span data-ttu-id="8406c-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati PostgreSQL usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="8406c-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="8406c-120">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="8406c-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8406c-121">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="8406c-122">Per creare una pipeline, è anche possibile usare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8406c-122">You can also use the following tools to create a pipeline:</span></span> 
    - <span data-ttu-id="8406c-123">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8406c-123">Azure portal</span></span>
    - <span data-ttu-id="8406c-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8406c-124">Visual Studio</span></span>
    - <span data-ttu-id="8406c-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8406c-125">Azure PowerShell</span></span>
    - <span data-ttu-id="8406c-126">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8406c-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="8406c-127">API .NET</span><span class="sxs-lookup"><span data-stu-id="8406c-127">.NET API</span></span>
    - <span data-ttu-id="8406c-128">API REST</span><span class="sxs-lookup"><span data-stu-id="8406c-128">REST API</span></span>

     <span data-ttu-id="8406c-129">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="8406c-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8406c-130">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="8406c-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="8406c-131">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="8406c-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8406c-132">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="8406c-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8406c-133">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="8406c-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8406c-134">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8406c-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8406c-135">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8406c-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8406c-136">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da un archivio dati PostgreSQL locale, vedere la sezione [Esempio JSON: Copiare dati da PostgreSQL a BLOB di Azure](#json-example-copy-data-from-postgresql-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8406c-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="8406c-137">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di un archivio dati PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="8406c-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8406c-138">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="8406c-138">Linked service properties</span></span>
<span data-ttu-id="8406c-139">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-139">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="8406c-140">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8406c-140">Property</span></span> | <span data-ttu-id="8406c-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8406c-141">Description</span></span> | <span data-ttu-id="8406c-142">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8406c-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8406c-143">type</span><span class="sxs-lookup"><span data-stu-id="8406c-143">type</span></span> |<span data-ttu-id="8406c-144">La proprietà type deve essere impostata su: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="8406c-144">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="8406c-145">Sì</span><span class="sxs-lookup"><span data-stu-id="8406c-145">Yes</span></span> |
| <span data-ttu-id="8406c-146">server</span><span class="sxs-lookup"><span data-stu-id="8406c-146">server</span></span> |<span data-ttu-id="8406c-147">Nome del server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-147">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="8406c-148">Sì</span><span class="sxs-lookup"><span data-stu-id="8406c-148">Yes</span></span> |
| <span data-ttu-id="8406c-149">database</span><span class="sxs-lookup"><span data-stu-id="8406c-149">database</span></span> |<span data-ttu-id="8406c-150">Nome del database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-150">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="8406c-151">Sì</span><span class="sxs-lookup"><span data-stu-id="8406c-151">Yes</span></span> |
| <span data-ttu-id="8406c-152">schema</span><span class="sxs-lookup"><span data-stu-id="8406c-152">schema</span></span> |<span data-ttu-id="8406c-153">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="8406c-153">Name of the schema in the database.</span></span> <span data-ttu-id="8406c-154">Il nome dello schema fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8406c-154">The schema name is case-sensitive.</span></span> |<span data-ttu-id="8406c-155">No</span><span class="sxs-lookup"><span data-stu-id="8406c-155">No</span></span> |
| <span data-ttu-id="8406c-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8406c-156">authenticationType</span></span> |<span data-ttu-id="8406c-157">Tipo di autenticazione usato per connettersi al database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-157">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="8406c-158">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="8406c-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8406c-159">Sì</span><span class="sxs-lookup"><span data-stu-id="8406c-159">Yes</span></span> |
| <span data-ttu-id="8406c-160">username</span><span class="sxs-lookup"><span data-stu-id="8406c-160">username</span></span> |<span data-ttu-id="8406c-161">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="8406c-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="8406c-162">No</span><span class="sxs-lookup"><span data-stu-id="8406c-162">No</span></span> |
| <span data-ttu-id="8406c-163">password</span><span class="sxs-lookup"><span data-stu-id="8406c-163">password</span></span> |<span data-ttu-id="8406c-164">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="8406c-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8406c-165">No</span><span class="sxs-lookup"><span data-stu-id="8406c-165">No</span></span> |
| <span data-ttu-id="8406c-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8406c-166">gatewayName</span></span> |<span data-ttu-id="8406c-167">Nome del gateway che il servizio Data factory deve usare per connettersi al database PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="8406c-167">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="8406c-168">Sì</span><span class="sxs-lookup"><span data-stu-id="8406c-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="8406c-169">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="8406c-169">Dataset properties</span></span>
<span data-ttu-id="8406c-170">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="8406c-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8406c-171">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="8406c-172">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-172">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8406c-173">La sezione typeProperties per il set di dati di tipo **RelationalTable** (che include il set di dati PostgreSQL) presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8406c-173">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="8406c-174">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8406c-174">Property</span></span> | <span data-ttu-id="8406c-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8406c-175">Description</span></span> | <span data-ttu-id="8406c-176">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8406c-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8406c-177">tableName</span><span class="sxs-lookup"><span data-stu-id="8406c-177">tableName</span></span> |<span data-ttu-id="8406c-178">Nome della tabella nell'istanza del database PostgreSQL a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="8406c-178">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="8406c-179">La proprietà tableName fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8406c-179">The tableName is case-sensitive.</span></span> |<span data-ttu-id="8406c-180">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="8406c-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8406c-181">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="8406c-181">Copy activity properties</span></span>
<span data-ttu-id="8406c-182">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8406c-182">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8406c-183">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="8406c-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="8406c-184">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="8406c-184">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="8406c-185">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="8406c-185">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8406c-186">Se l'origine è di tipo **RelationalSource** (che comprende PostgreSQL), sono disponibili le proprietà seguenti nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="8406c-186">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="8406c-187">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8406c-187">Property</span></span> | <span data-ttu-id="8406c-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8406c-188">Description</span></span> | <span data-ttu-id="8406c-189">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="8406c-189">Allowed values</span></span> | <span data-ttu-id="8406c-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8406c-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8406c-191">query</span><span class="sxs-lookup"><span data-stu-id="8406c-191">query</span></span> |<span data-ttu-id="8406c-192">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-192">Use the custom query to read data.</span></span> |<span data-ttu-id="8406c-193">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-193">SQL query string.</span></span> <span data-ttu-id="8406c-194">Ad esempio: "query": "select * from \"Schema\".\"Tabella\"".</span><span class="sxs-lookup"><span data-stu-id="8406c-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="8406c-195">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="8406c-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="8406c-196">I nomi di schemi e tabelle fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8406c-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="8406c-197">Racchiudere i nomi tra `""` (virgolette doppie) nella query.</span><span class="sxs-lookup"><span data-stu-id="8406c-197">Enclose them in `""` (double quotes) in the query.</span></span>  

<span data-ttu-id="8406c-198">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="8406c-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="8406c-199">Esempio JSON: Copiare dati da PostgreSQL a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8406c-199">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="8406c-200">Questo esempio fornisce le definizioni JSON di esempio da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8406c-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8406c-201">Illustrano come copiare dati da un database PostgreSQL in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8406c-201">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="8406c-202">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8406c-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="8406c-203">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="8406c-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="8406c-204">Non include istruzioni dettagliate per la creazione della data factory.</span><span class="sxs-lookup"><span data-stu-id="8406c-204">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="8406c-205">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="8406c-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="8406c-206">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="8406c-206">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="8406c-207">Un servizio collegato di tipo [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8406c-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8406c-208">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8406c-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8406c-209">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8406c-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8406c-210">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8406c-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8406c-211">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8406c-211">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8406c-212">L'esempio copia i dati dai risultati della query nel database PostgreSQL in un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8406c-212">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="8406c-213">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="8406c-213">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8406c-214">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8406c-214">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="8406c-215">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="8406c-215">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8406c-216">**Servizio collegato PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="8406c-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="8406c-217">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="8406c-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="8406c-218">**Set di dati di input PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="8406c-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="8406c-219">L'esempio presuppone che sia stata creata una tabella "MyTable" in PostgreSQL e che contenga una colonna denominata "timestamp" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="8406c-219">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="8406c-220">L'impostazione `"external": true` comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è generato da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="8406c-220">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

<span data-ttu-id="8406c-221">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="8406c-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8406c-222">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="8406c-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8406c-223">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="8406c-223">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8406c-224">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="8406c-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="8406c-225">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="8406c-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="8406c-226">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8406c-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="8406c-227">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8406c-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="8406c-228">La query SQL specificata per la proprietà **query** seleziona i dati dalla tabella public.usstates nel database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8406c-228">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="8406c-229">Mapping dei tipi per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8406c-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="8406c-230">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="8406c-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="8406c-231">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="8406c-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="8406c-232">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="8406c-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="8406c-233">Quando si spostano i dati in PostgreSQL vengono usati i mapping seguenti dal tipo PostgreSQL al tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="8406c-233">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="8406c-234">Tipo di database PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8406c-234">PostgreSQL Database type</span></span> | <span data-ttu-id="8406c-235">Alias PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="8406c-235">PostgresSQL aliases</span></span> | <span data-ttu-id="8406c-236">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8406c-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8406c-237">abstime</span><span class="sxs-lookup"><span data-stu-id="8406c-237">abstime</span></span> | |<span data-ttu-id="8406c-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="8406c-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="8406c-239">bigint</span><span class="sxs-lookup"><span data-stu-id="8406c-239">bigint</span></span> |<span data-ttu-id="8406c-240">int8</span><span class="sxs-lookup"><span data-stu-id="8406c-240">int8</span></span> |<span data-ttu-id="8406c-241">Int64</span><span class="sxs-lookup"><span data-stu-id="8406c-241">Int64</span></span> |
| <span data-ttu-id="8406c-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="8406c-242">bigserial</span></span> |<span data-ttu-id="8406c-243">serial8</span><span class="sxs-lookup"><span data-stu-id="8406c-243">serial8</span></span> |<span data-ttu-id="8406c-244">Int64</span><span class="sxs-lookup"><span data-stu-id="8406c-244">Int64</span></span> |
| <span data-ttu-id="8406c-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-245">bit [ (n) ]</span></span> | |<span data-ttu-id="8406c-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="8406c-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="8406c-248">varbit</span><span class="sxs-lookup"><span data-stu-id="8406c-248">varbit</span></span> |<span data-ttu-id="8406c-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-249">Byte[], String</span></span> |
| <span data-ttu-id="8406c-250">boolean</span><span class="sxs-lookup"><span data-stu-id="8406c-250">boolean</span></span> |<span data-ttu-id="8406c-251">bool</span><span class="sxs-lookup"><span data-stu-id="8406c-251">bool</span></span> |<span data-ttu-id="8406c-252">boolean</span><span class="sxs-lookup"><span data-stu-id="8406c-252">Boolean</span></span> |
| <span data-ttu-id="8406c-253">box</span><span class="sxs-lookup"><span data-stu-id="8406c-253">box</span></span> | |<span data-ttu-id="8406c-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-255">bytea</span><span class="sxs-lookup"><span data-stu-id="8406c-255">bytea</span></span> | |<span data-ttu-id="8406c-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-257">character [ (n) ]</span></span> |<span data-ttu-id="8406c-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-258">char [ (n) ]</span></span> |<span data-ttu-id="8406c-259">String</span><span class="sxs-lookup"><span data-stu-id="8406c-259">String</span></span> |
| <span data-ttu-id="8406c-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-260">character varying [ (n) ]</span></span> |<span data-ttu-id="8406c-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-261">varchar [ (n) ]</span></span> |<span data-ttu-id="8406c-262">String</span><span class="sxs-lookup"><span data-stu-id="8406c-262">String</span></span> |
| <span data-ttu-id="8406c-263">cid</span><span class="sxs-lookup"><span data-stu-id="8406c-263">cid</span></span> | |<span data-ttu-id="8406c-264">String</span><span class="sxs-lookup"><span data-stu-id="8406c-264">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-265">cidr</span><span class="sxs-lookup"><span data-stu-id="8406c-265">cidr</span></span> | |<span data-ttu-id="8406c-266">String</span><span class="sxs-lookup"><span data-stu-id="8406c-266">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-267">circle</span><span class="sxs-lookup"><span data-stu-id="8406c-267">circle</span></span> | |<span data-ttu-id="8406c-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-269">date</span><span class="sxs-lookup"><span data-stu-id="8406c-269">date</span></span> | |<span data-ttu-id="8406c-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="8406c-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="8406c-271">daterange</span><span class="sxs-lookup"><span data-stu-id="8406c-271">daterange</span></span> | |<span data-ttu-id="8406c-272">String</span><span class="sxs-lookup"><span data-stu-id="8406c-272">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-273">double precision</span><span class="sxs-lookup"><span data-stu-id="8406c-273">double precision</span></span> |<span data-ttu-id="8406c-274">float8</span><span class="sxs-lookup"><span data-stu-id="8406c-274">float8</span></span> |<span data-ttu-id="8406c-275">Double</span><span class="sxs-lookup"><span data-stu-id="8406c-275">Double</span></span> |
| <span data-ttu-id="8406c-276">inet</span><span class="sxs-lookup"><span data-stu-id="8406c-276">inet</span></span> | |<span data-ttu-id="8406c-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-278">intarry</span><span class="sxs-lookup"><span data-stu-id="8406c-278">intarry</span></span> | |<span data-ttu-id="8406c-279">String</span><span class="sxs-lookup"><span data-stu-id="8406c-279">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-280">int4range</span><span class="sxs-lookup"><span data-stu-id="8406c-280">int4range</span></span> | |<span data-ttu-id="8406c-281">String</span><span class="sxs-lookup"><span data-stu-id="8406c-281">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-282">int8range</span><span class="sxs-lookup"><span data-stu-id="8406c-282">int8range</span></span> | |<span data-ttu-id="8406c-283">String</span><span class="sxs-lookup"><span data-stu-id="8406c-283">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-284">integer</span><span class="sxs-lookup"><span data-stu-id="8406c-284">integer</span></span> |<span data-ttu-id="8406c-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="8406c-285">int, int4</span></span> |<span data-ttu-id="8406c-286">Int32</span><span class="sxs-lookup"><span data-stu-id="8406c-286">Int32</span></span> |
| <span data-ttu-id="8406c-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="8406c-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8406c-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="8406c-289">json</span><span class="sxs-lookup"><span data-stu-id="8406c-289">json</span></span> | |<span data-ttu-id="8406c-290">String</span><span class="sxs-lookup"><span data-stu-id="8406c-290">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="8406c-291">jsonb</span></span> | |<span data-ttu-id="8406c-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8406c-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="8406c-293">line</span><span class="sxs-lookup"><span data-stu-id="8406c-293">line</span></span> | |<span data-ttu-id="8406c-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-295">lseg</span><span class="sxs-lookup"><span data-stu-id="8406c-295">lseg</span></span> | |<span data-ttu-id="8406c-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="8406c-297">macaddr</span></span> | |<span data-ttu-id="8406c-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-299">money</span><span class="sxs-lookup"><span data-stu-id="8406c-299">money</span></span> | |<span data-ttu-id="8406c-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="8406c-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="8406c-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="8406c-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="8406c-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="8406c-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="8406c-303">Decimal</span></span> |
| <span data-ttu-id="8406c-304">numrange</span><span class="sxs-lookup"><span data-stu-id="8406c-304">numrange</span></span> | |<span data-ttu-id="8406c-305">String</span><span class="sxs-lookup"><span data-stu-id="8406c-305">String</span></span> |&nbsp;
| <span data-ttu-id="8406c-306">oid</span><span class="sxs-lookup"><span data-stu-id="8406c-306">oid</span></span> | |<span data-ttu-id="8406c-307">Int32</span><span class="sxs-lookup"><span data-stu-id="8406c-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="8406c-308">path</span><span class="sxs-lookup"><span data-stu-id="8406c-308">path</span></span> | |<span data-ttu-id="8406c-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="8406c-310">pg_lsn</span></span> | |<span data-ttu-id="8406c-311">Int64</span><span class="sxs-lookup"><span data-stu-id="8406c-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="8406c-312">point</span><span class="sxs-lookup"><span data-stu-id="8406c-312">point</span></span> | |<span data-ttu-id="8406c-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-314">polygon</span><span class="sxs-lookup"><span data-stu-id="8406c-314">polygon</span></span> | |<span data-ttu-id="8406c-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="8406c-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="8406c-316">real</span><span class="sxs-lookup"><span data-stu-id="8406c-316">real</span></span> |<span data-ttu-id="8406c-317">float4</span><span class="sxs-lookup"><span data-stu-id="8406c-317">float4</span></span> |<span data-ttu-id="8406c-318">Single</span><span class="sxs-lookup"><span data-stu-id="8406c-318">Single</span></span> |
| <span data-ttu-id="8406c-319">smallint</span><span class="sxs-lookup"><span data-stu-id="8406c-319">smallint</span></span> |<span data-ttu-id="8406c-320">int2</span><span class="sxs-lookup"><span data-stu-id="8406c-320">int2</span></span> |<span data-ttu-id="8406c-321">Int16</span><span class="sxs-lookup"><span data-stu-id="8406c-321">Int16</span></span> |
| <span data-ttu-id="8406c-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="8406c-322">smallserial</span></span> |<span data-ttu-id="8406c-323">serial2</span><span class="sxs-lookup"><span data-stu-id="8406c-323">serial2</span></span> |<span data-ttu-id="8406c-324">Int16</span><span class="sxs-lookup"><span data-stu-id="8406c-324">Int16</span></span> |
| <span data-ttu-id="8406c-325">serial</span><span class="sxs-lookup"><span data-stu-id="8406c-325">serial</span></span> |<span data-ttu-id="8406c-326">serial4</span><span class="sxs-lookup"><span data-stu-id="8406c-326">serial4</span></span> |<span data-ttu-id="8406c-327">Int32</span><span class="sxs-lookup"><span data-stu-id="8406c-327">Int32</span></span> |
| <span data-ttu-id="8406c-328">text</span><span class="sxs-lookup"><span data-stu-id="8406c-328">text</span></span> | |<span data-ttu-id="8406c-329">String</span><span class="sxs-lookup"><span data-stu-id="8406c-329">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="8406c-330">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="8406c-330">Map source to sink columns</span></span>
<span data-ttu-id="8406c-331">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8406c-331">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8406c-332">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="8406c-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="8406c-333">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="8406c-333">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="8406c-334">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="8406c-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8406c-335">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="8406c-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8406c-336">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="8406c-336">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="8406c-337">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8406c-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8406c-338">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="8406c-338">Performance and Tuning</span></span>
<span data-ttu-id="8406c-339">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8406c-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
