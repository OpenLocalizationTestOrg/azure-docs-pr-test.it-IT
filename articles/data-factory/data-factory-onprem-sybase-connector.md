---
title: Spostare dati da Sybase usando Azure Data Factory | Documentazione Microsoft
description: Informazioni su come spostare i dati dal Database di Sybase utilizzando Data factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="f9c9d-103">Spostare i dati da Sybase utilizzando Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="f9c9d-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="f9c9d-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un database Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="f9c9d-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="f9c9d-106">È possibile copiare dati da un archivio dati Sybase locale a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="f9c9d-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f9c9d-108">Data Factory supporta attualmente solo lo spostamento dei dati da un archivio dati Sybase ad altri archivi dati, ma non da altri archivi dati a un archivio dati Sybase.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f9c9d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f9c9d-109">Prerequisites</span></span>
<span data-ttu-id="f9c9d-110">Data factory supporta la connessione a origini Sybase locali tramite il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="f9c9d-111">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="f9c9d-112">Il gateway è necessario anche se il database Sybase è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="f9c9d-113">È possibile installare il gateway nella stessa VM IaaS dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c9d-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="f9c9d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="f9c9d-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="f9c9d-115">Supported versions and installation</span></span>
<span data-ttu-id="f9c9d-116">Perché Gateway di gestione dati si connetta al database Sybase, è necessario installare il [provider di dati per Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 o versione successiva nello stesso sistema del Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="f9c9d-117">Sono supportate le versioni di Sybase a partire dalla 16.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f9c9d-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f9c9d-118">Getting started</span></span>
<span data-ttu-id="f9c9d-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="f9c9d-120">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f9c9d-121">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="f9c9d-122">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f9c9d-123">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f9c9d-124">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="f9c9d-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="f9c9d-125">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f9c9d-126">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="f9c9d-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f9c9d-128">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f9c9d-129">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f9c9d-130">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da un archivio dati Sybase locale, vedere la sezione [Esempio JSON: Copiare dati da Sybase a BLOB di Azure](#json-example-copy-data-from-sybase-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f9c9d-131">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un archivio dati Sybase:</span><span class="sxs-lookup"><span data-stu-id="f9c9d-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f9c9d-132">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="f9c9d-132">Linked service properties</span></span>
<span data-ttu-id="f9c9d-133">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato Sybase.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="f9c9d-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f9c9d-134">Property</span></span> | <span data-ttu-id="f9c9d-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f9c9d-135">Description</span></span> | <span data-ttu-id="f9c9d-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f9c9d-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9c9d-137">type</span><span class="sxs-lookup"><span data-stu-id="f9c9d-137">type</span></span> |<span data-ttu-id="f9c9d-138">La proprietà del tipo deve essere impostata su: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="f9c9d-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="f9c9d-139">Sì</span><span class="sxs-lookup"><span data-stu-id="f9c9d-139">Yes</span></span> |
| <span data-ttu-id="f9c9d-140">server</span><span class="sxs-lookup"><span data-stu-id="f9c9d-140">server</span></span> |<span data-ttu-id="f9c9d-141">Nome del server Sybase.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-141">Name of the Sybase server.</span></span> |<span data-ttu-id="f9c9d-142">Sì</span><span class="sxs-lookup"><span data-stu-id="f9c9d-142">Yes</span></span> |
| <span data-ttu-id="f9c9d-143">database</span><span class="sxs-lookup"><span data-stu-id="f9c9d-143">database</span></span> |<span data-ttu-id="f9c9d-144">Nome del database Sybase.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-144">Name of the Sybase database.</span></span> |<span data-ttu-id="f9c9d-145">Sì</span><span class="sxs-lookup"><span data-stu-id="f9c9d-145">Yes</span></span> |
| <span data-ttu-id="f9c9d-146">schema</span><span class="sxs-lookup"><span data-stu-id="f9c9d-146">schema</span></span> |<span data-ttu-id="f9c9d-147">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-147">Name of the schema in the database.</span></span> |<span data-ttu-id="f9c9d-148">No</span><span class="sxs-lookup"><span data-stu-id="f9c9d-148">No</span></span> |
| <span data-ttu-id="f9c9d-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f9c9d-149">authenticationType</span></span> |<span data-ttu-id="f9c9d-150">Tipo di autenticazione usato per connettersi al database Sybase.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="f9c9d-151">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="f9c9d-152">Sì</span><span class="sxs-lookup"><span data-stu-id="f9c9d-152">Yes</span></span> |
| <span data-ttu-id="f9c9d-153">username</span><span class="sxs-lookup"><span data-stu-id="f9c9d-153">username</span></span> |<span data-ttu-id="f9c9d-154">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="f9c9d-155">No</span><span class="sxs-lookup"><span data-stu-id="f9c9d-155">No</span></span> |
| <span data-ttu-id="f9c9d-156">password</span><span class="sxs-lookup"><span data-stu-id="f9c9d-156">password</span></span> |<span data-ttu-id="f9c9d-157">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="f9c9d-158">No</span><span class="sxs-lookup"><span data-stu-id="f9c9d-158">No</span></span> |
| <span data-ttu-id="f9c9d-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f9c9d-159">gatewayName</span></span> |<span data-ttu-id="f9c9d-160">Nome del gateway che il servizio Data factory deve usare per connettersi al database Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="f9c9d-161">Sì</span><span class="sxs-lookup"><span data-stu-id="f9c9d-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f9c9d-162">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="f9c9d-162">Dataset properties</span></span>
<span data-ttu-id="f9c9d-163">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f9c9d-164">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f9c9d-165">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f9c9d-166">La sezione **typeProperties** per il set di dati di tipo **RelationalTable** (che include il set di dati Sybase) presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9c9d-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="f9c9d-167">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f9c9d-167">Property</span></span> | <span data-ttu-id="f9c9d-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f9c9d-168">Description</span></span> | <span data-ttu-id="f9c9d-169">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f9c9d-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9c9d-170">tableName</span><span class="sxs-lookup"><span data-stu-id="f9c9d-170">tableName</span></span> |<span data-ttu-id="f9c9d-171">Nome della tabella nell'istanza del database Sybase a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="f9c9d-172">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="f9c9d-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f9c9d-173">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="f9c9d-173">Copy activity properties</span></span>
<span data-ttu-id="f9c9d-174">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f9c9d-175">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f9c9d-176">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="f9c9d-177">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f9c9d-178">Se l'origine è di tipo **RelationalSource** (che include Sybase), nella sezione **typeProperties** sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9c9d-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="f9c9d-179">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f9c9d-179">Property</span></span> | <span data-ttu-id="f9c9d-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f9c9d-180">Description</span></span> | <span data-ttu-id="f9c9d-181">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="f9c9d-181">Allowed values</span></span> | <span data-ttu-id="f9c9d-182">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f9c9d-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9c9d-183">query</span><span class="sxs-lookup"><span data-stu-id="f9c9d-183">query</span></span> |<span data-ttu-id="f9c9d-184">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-184">Use the custom query to read data.</span></span> |<span data-ttu-id="f9c9d-185">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-185">SQL query string.</span></span> <span data-ttu-id="f9c9d-186">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="f9c9d-187">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="f9c9d-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="f9c9d-188">Esempio JSON: Copiare dati da Sybase a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="f9c9d-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="f9c9d-189">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f9c9d-190">Illustrano come copiare dati da un database Sybase in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="f9c9d-191">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="f9c9d-192">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9c9d-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="f9c9d-193">Un servizio collegato di tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="f9c9d-194">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f9c9d-195">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f9c9d-196">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f9c9d-197">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f9c9d-198">L'esempio copia i dati dai risultati della query nel database Sybase in un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="f9c9d-199">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f9c9d-200">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="f9c9d-201">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="f9c9d-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f9c9d-202">**Servizio collegato Sybase:**</span><span class="sxs-lookup"><span data-stu-id="f9c9d-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="f9c9d-203">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="f9c9d-203">**Azure Blob storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="f9c9d-204">**Set di dati di input Sybase:**</span><span class="sxs-lookup"><span data-stu-id="f9c9d-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="f9c9d-205">L'esempio presuppone che sia stata creata una tabella "MyTable" in Sybase e che contenga una colonna denominata "timestamp" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="f9c9d-206">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="f9c9d-207">Si noti che il valore **type** del servizio collegato è impostato su **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="f9c9d-208">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="f9c9d-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f9c9d-209">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f9c9d-210">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f9c9d-211">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="f9c9d-212">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="f9c9d-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="f9c9d-213">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="f9c9d-214">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f9c9d-215">La query SQL specificata per la proprietà **query** seleziona i dati dalla tabella DBA.Orders nel database.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="f9c9d-216">Mapping dei tipi per Sybase</span><span class="sxs-lookup"><span data-stu-id="f9c9d-216">Type mapping for Sybase</span></span>
<span data-ttu-id="f9c9d-217">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="f9c9d-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f9c9d-218">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="f9c9d-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f9c9d-219">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="f9c9d-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f9c9d-220">Sybase supporta i tipi T-SQL e T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="f9c9d-221">Per una tabella di mapping dai tipi SQL al tipo .NET, vedere l'articolo [Connettore SQL Azure](data-factory-azure-sql-connector.md) .</span><span class="sxs-lookup"><span data-stu-id="f9c9d-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="f9c9d-222">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="f9c9d-222">Map source to sink columns</span></span>
<span data-ttu-id="f9c9d-223">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f9c9d-224">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="f9c9d-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="f9c9d-225">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f9c9d-226">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f9c9d-227">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f9c9d-228">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="f9c9d-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f9c9d-229">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f9c9d-230">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="f9c9d-230">Performance and Tuning</span></span>
<span data-ttu-id="f9c9d-231">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f9c9d-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
