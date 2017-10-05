---
title: Spostare dati da SAP Business Warehouse usando Azure Data Factory | Microsoft Docs
description: Informazioni su come spostare dati da SAP Business Warehouse usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="a03bf-103">Spostare dati da SAP Business Warehouse usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a03bf-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="a03bf-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un database SAP Business Warehouse (BW) locale.</span><span class="sxs-lookup"><span data-stu-id="a03bf-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="a03bf-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a03bf-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="a03bf-106">È possibile copiare dati da un archivio dati SAP Business Warehouse locale a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="a03bf-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="a03bf-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a03bf-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a03bf-108">Data Factory supporta attualmente solo lo spostamento di dati da SAP Business Warehouse ad altri archivi dati, non da altri archivi dati a un SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a03bf-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="a03bf-109">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="a03bf-109">Supported versions and installation</span></span>
<span data-ttu-id="a03bf-110">Questo connettore supporta SAP Business Warehouse versione 7.x.</span><span class="sxs-lookup"><span data-stu-id="a03bf-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="a03bf-111">Supporta anche la copia di dati da Infocube e QueryCubes (incluse query BEx) tramite query MDX.</span><span class="sxs-lookup"><span data-stu-id="a03bf-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="a03bf-112">Per abilitare la connettività all'istanza di SAP BW, installare i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a03bf-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="a03bf-113">**Gateway di gestione dati**: il servizio Data Factory supporta la connessione ad archivi dati locali (incluso SAP Business Warehouse) usando un componente denominato Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="a03bf-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="a03bf-114">Per informazioni su Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway, vedere l'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="a03bf-115">Il gateway è necessario anche se il database SAP Business Warehouse è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="a03bf-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="a03bf-116">È possibile installare il gateway nella stessa VM dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="a03bf-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="a03bf-117">**Libreria SAP NetWeaver** nel computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="a03bf-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="a03bf-118">È possibile ottenere la libreria SAP Netweaver dal proprio amministratore SAP o direttamente dall'[area per il download di software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="a03bf-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="a03bf-119">Per ottenere il percorso di download della versione più recente, cercare **SAP Note #1025361**.</span><span class="sxs-lookup"><span data-stu-id="a03bf-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="a03bf-120">Assicurarsi che l'architettura della libreria SAP NetWeaver (32 bit o 64 bit) corrisponda al tipo di installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="a03bf-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="a03bf-121">Installare quindi tutti i file inclusi in SAP NetWeaver RFC SDK in base alla nota SAP.</span><span class="sxs-lookup"><span data-stu-id="a03bf-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="a03bf-122">La libreria SAP NetWeaver è inclusa anche nell'installazione degli strumenti client SAP.</span><span class="sxs-lookup"><span data-stu-id="a03bf-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="a03bf-123">Inserire le DLL estratte dall'SDK di NetWeaver RFC nella cartella system32.</span><span class="sxs-lookup"><span data-stu-id="a03bf-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a03bf-124">introduttiva</span><span class="sxs-lookup"><span data-stu-id="a03bf-124">Getting started</span></span>
<span data-ttu-id="a03bf-125">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="a03bf-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a03bf-126">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="a03bf-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a03bf-127">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="a03bf-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="a03bf-128">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="a03bf-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a03bf-129">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="a03bf-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a03bf-130">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="a03bf-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="a03bf-131">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="a03bf-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a03bf-132">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="a03bf-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a03bf-133">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="a03bf-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a03bf-134">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a03bf-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a03bf-135">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a03bf-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a03bf-136">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da un SAP Business Warehouse locale, vedere la sezione [Esempio JSON: Copiare dati da SAP Business Warehouse a BLOB di Azure](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a03bf-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a03bf-137">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di un archivio dati SAP BW:</span><span class="sxs-lookup"><span data-stu-id="a03bf-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a03bf-138">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="a03bf-138">Linked service properties</span></span>
<span data-ttu-id="a03bf-139">La tabella seguente fornisce la descrizione degli elementi JSON specifici del servizio collegato SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="a03bf-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="a03bf-140">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a03bf-140">Property</span></span> | <span data-ttu-id="a03bf-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a03bf-141">Description</span></span> | <span data-ttu-id="a03bf-142">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="a03bf-142">Allowed values</span></span> | <span data-ttu-id="a03bf-143">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="a03bf-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="a03bf-144">server</span><span class="sxs-lookup"><span data-stu-id="a03bf-144">server</span></span> | <span data-ttu-id="a03bf-145">Nome del server in cui si trova l'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="a03bf-146">string</span><span class="sxs-lookup"><span data-stu-id="a03bf-146">string</span></span> | <span data-ttu-id="a03bf-147">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-147">Yes</span></span>
<span data-ttu-id="a03bf-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="a03bf-148">systemNumber</span></span> | <span data-ttu-id="a03bf-149">Numero del sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="a03bf-150">Numero decimale a due cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="a03bf-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="a03bf-151">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-151">Yes</span></span>
<span data-ttu-id="a03bf-152">clientId</span><span class="sxs-lookup"><span data-stu-id="a03bf-152">clientId</span></span> | <span data-ttu-id="a03bf-153">ID del client nel sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="a03bf-154">Numero decimale a tre cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="a03bf-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="a03bf-155">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-155">Yes</span></span>
<span data-ttu-id="a03bf-156">username</span><span class="sxs-lookup"><span data-stu-id="a03bf-156">username</span></span> | <span data-ttu-id="a03bf-157">Nome dell'utente che ha accesso al server SAP</span><span class="sxs-lookup"><span data-stu-id="a03bf-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="a03bf-158">string</span><span class="sxs-lookup"><span data-stu-id="a03bf-158">string</span></span> | <span data-ttu-id="a03bf-159">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-159">Yes</span></span>
<span data-ttu-id="a03bf-160">password</span><span class="sxs-lookup"><span data-stu-id="a03bf-160">password</span></span> | <span data-ttu-id="a03bf-161">Password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="a03bf-161">Password for the user.</span></span> | <span data-ttu-id="a03bf-162">string</span><span class="sxs-lookup"><span data-stu-id="a03bf-162">string</span></span> | <span data-ttu-id="a03bf-163">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-163">Yes</span></span>
<span data-ttu-id="a03bf-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a03bf-164">gatewayName</span></span> | <span data-ttu-id="a03bf-165">Nome del gateway che il servizio Data factory deve usare per connettersi all'istanza di SAP BW locale.</span><span class="sxs-lookup"><span data-stu-id="a03bf-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="a03bf-166">string</span><span class="sxs-lookup"><span data-stu-id="a03bf-166">string</span></span> | <span data-ttu-id="a03bf-167">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-167">Yes</span></span>
<span data-ttu-id="a03bf-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a03bf-168">encryptedCredential</span></span> | <span data-ttu-id="a03bf-169">Stringa di credenziali crittografata.</span><span class="sxs-lookup"><span data-stu-id="a03bf-169">The encrypted credential string.</span></span> | <span data-ttu-id="a03bf-170">string</span><span class="sxs-lookup"><span data-stu-id="a03bf-170">string</span></span> | <span data-ttu-id="a03bf-171">No</span><span class="sxs-lookup"><span data-stu-id="a03bf-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="a03bf-172">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="a03bf-172">Dataset properties</span></span>
<span data-ttu-id="a03bf-173">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a03bf-174">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="a03bf-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a03bf-175">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="a03bf-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a03bf-176">Il set di dati SAP BW di tipo **RelationalTable** non supporta alcuna proprietà specifica del tipo.</span><span class="sxs-lookup"><span data-stu-id="a03bf-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="a03bf-177">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="a03bf-177">Copy activity properties</span></span>
<span data-ttu-id="a03bf-178">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a03bf-179">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="a03bf-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="a03bf-180">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="a03bf-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="a03bf-181">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="a03bf-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a03bf-182">Se l'origine nell'attività di copia è di tipo **RelationalSource** (che include SAP BW), nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a03bf-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a03bf-183">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a03bf-183">Property</span></span> | <span data-ttu-id="a03bf-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a03bf-184">Description</span></span> | <span data-ttu-id="a03bf-185">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="a03bf-185">Allowed values</span></span> | <span data-ttu-id="a03bf-186">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a03bf-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a03bf-187">query</span><span class="sxs-lookup"><span data-stu-id="a03bf-187">query</span></span> | <span data-ttu-id="a03bf-188">Specifica la query MDX che consente di leggere i dati dall'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="a03bf-189">Query MDX.</span><span class="sxs-lookup"><span data-stu-id="a03bf-189">MDX query.</span></span> | <span data-ttu-id="a03bf-190">Sì</span><span class="sxs-lookup"><span data-stu-id="a03bf-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="a03bf-191">Esempio JSON: Copiare dati da SAP Business Warehouse a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="a03bf-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="a03bf-192">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a03bf-193">Questo esempio illustra come copiare dati da un database SAP Business Warehouse locale a un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a03bf-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="a03bf-194">Tuttavia, i dati possono essere copiati **direttamente** in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a03bf-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a03bf-195">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="a03bf-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="a03bf-196">Non include istruzioni dettagliate per la creazione della data factory.</span><span class="sxs-lookup"><span data-stu-id="a03bf-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="a03bf-197">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="a03bf-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="a03bf-198">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="a03bf-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="a03bf-199">Un servizio collegato di tipo [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a03bf-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="a03bf-200">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a03bf-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a03bf-201">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a03bf-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a03bf-202">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a03bf-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a03bf-203">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a03bf-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a03bf-204">Nell'esempio i dati vengono copiati da un'istanza di SAP Business Warehouse a un BLOB di Azure a intervalli orari.</span><span class="sxs-lookup"><span data-stu-id="a03bf-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="a03bf-205">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="a03bf-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a03bf-206">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="a03bf-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="a03bf-207">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="a03bf-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="a03bf-208">Servizio collegato SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="a03bf-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="a03bf-209">Questo servizio collegato collega l'istanza di SAP BW alla data factory.</span><span class="sxs-lookup"><span data-stu-id="a03bf-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="a03bf-210">La proprietà type è impostata su **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="a03bf-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="a03bf-211">La sezione typeProperties fornisce informazioni di connessione per l'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="a03bf-212">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a03bf-212">Azure Storage linked service</span></span>
<span data-ttu-id="a03bf-213">Questo servizio collegato collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="a03bf-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="a03bf-214">La proprietà type è impostata su **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="a03bf-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="a03bf-215">La sezione typeProperties fornisce informazioni di connessione per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a03bf-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="a03bf-216">Set di dati di input SAP BW</span><span class="sxs-lookup"><span data-stu-id="a03bf-216">SAP BW input dataset</span></span>
<span data-ttu-id="a03bf-217">Questo set di dati definisce il set di dati SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a03bf-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="a03bf-218">Per il set di dati Data Factory il tipo deve essere impostato su **RelationalTable**,</span><span class="sxs-lookup"><span data-stu-id="a03bf-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="a03bf-219">mentre per il set di dati SAP BW non è attualmente necessario specificare alcuna proprietà relativa al tipo.</span><span class="sxs-lookup"><span data-stu-id="a03bf-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="a03bf-220">La query presente nella definizione dell'attività di copia specifica i dati da leggere dall'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="a03bf-221">Impostando la proprietà esterna su true si comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="a03bf-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="a03bf-222">Le proprietà di frequenza e intervallo definiscono la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a03bf-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="a03bf-223">In questo caso, i dati vengono letti dall'istanza di SAP BW ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a03bf-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a03bf-224">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="a03bf-224">Azure Blob output dataset</span></span>
<span data-ttu-id="a03bf-225">Questo set di dati definisce il set di dati di output di BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a03bf-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="a03bf-226">La proprietà type è impostata su AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="a03bf-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="a03bf-227">La sezione typeProperties specifica dove devono essere archiviati i dati copiati dall'istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="a03bf-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="a03bf-228">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="a03bf-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a03bf-229">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a03bf-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a03bf-230">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="a03bf-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="a03bf-231">Pipeline con attività di copia</span><span class="sxs-lookup"><span data-stu-id="a03bf-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="a03bf-232">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="a03bf-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a03bf-233">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** (per l'origine SAP BW) e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a03bf-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a03bf-234">La query specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="a03bf-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="a03bf-235">Mapping dei tipi per SAP BW</span><span class="sxs-lookup"><span data-stu-id="a03bf-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="a03bf-236">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="a03bf-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="a03bf-237">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="a03bf-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a03bf-238">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="a03bf-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a03bf-239">Quando si spostano dati da SAP BW, vengono usati i mapping seguenti tra i tipi SAP BW e i tipi .NET.</span><span class="sxs-lookup"><span data-stu-id="a03bf-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="a03bf-240">Tipo di dati nel dizionario ABAP</span><span class="sxs-lookup"><span data-stu-id="a03bf-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="a03bf-241">Tipo di dati .Net</span><span class="sxs-lookup"><span data-stu-id="a03bf-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="a03bf-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="a03bf-242">ACCP</span></span> |  <span data-ttu-id="a03bf-243">int</span><span class="sxs-lookup"><span data-stu-id="a03bf-243">Int</span></span>
<span data-ttu-id="a03bf-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="a03bf-244">CHAR</span></span> | <span data-ttu-id="a03bf-245">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-245">String</span></span>
<span data-ttu-id="a03bf-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="a03bf-246">CLNT</span></span> | <span data-ttu-id="a03bf-247">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-247">String</span></span>
<span data-ttu-id="a03bf-248">CURR</span><span class="sxs-lookup"><span data-stu-id="a03bf-248">CURR</span></span> | <span data-ttu-id="a03bf-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03bf-249">Decimal</span></span>
<span data-ttu-id="a03bf-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="a03bf-250">CUKY</span></span> | <span data-ttu-id="a03bf-251">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-251">String</span></span>
<span data-ttu-id="a03bf-252">DEC</span><span class="sxs-lookup"><span data-stu-id="a03bf-252">DEC</span></span> | <span data-ttu-id="a03bf-253">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03bf-253">Decimal</span></span>
<span data-ttu-id="a03bf-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="a03bf-254">FLTP</span></span> | <span data-ttu-id="a03bf-255">Double</span><span class="sxs-lookup"><span data-stu-id="a03bf-255">Double</span></span>
<span data-ttu-id="a03bf-256">INT1</span><span class="sxs-lookup"><span data-stu-id="a03bf-256">INT1</span></span> | <span data-ttu-id="a03bf-257">Byte</span><span class="sxs-lookup"><span data-stu-id="a03bf-257">Byte</span></span>
<span data-ttu-id="a03bf-258">INT2</span><span class="sxs-lookup"><span data-stu-id="a03bf-258">INT2</span></span> | <span data-ttu-id="a03bf-259">Int16</span><span class="sxs-lookup"><span data-stu-id="a03bf-259">Int16</span></span>
<span data-ttu-id="a03bf-260">INT4</span><span class="sxs-lookup"><span data-stu-id="a03bf-260">INT4</span></span> | <span data-ttu-id="a03bf-261">int</span><span class="sxs-lookup"><span data-stu-id="a03bf-261">Int</span></span>
<span data-ttu-id="a03bf-262">LANG</span><span class="sxs-lookup"><span data-stu-id="a03bf-262">LANG</span></span> | <span data-ttu-id="a03bf-263">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-263">String</span></span>
<span data-ttu-id="a03bf-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="a03bf-264">LCHR</span></span> | <span data-ttu-id="a03bf-265">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-265">String</span></span>
<span data-ttu-id="a03bf-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="a03bf-266">LRAW</span></span> | <span data-ttu-id="a03bf-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a03bf-267">Byte[]</span></span>
<span data-ttu-id="a03bf-268">PREC</span><span class="sxs-lookup"><span data-stu-id="a03bf-268">PREC</span></span> | <span data-ttu-id="a03bf-269">Int16</span><span class="sxs-lookup"><span data-stu-id="a03bf-269">Int16</span></span>
<span data-ttu-id="a03bf-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="a03bf-270">QUAN</span></span> | <span data-ttu-id="a03bf-271">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03bf-271">Decimal</span></span>
<span data-ttu-id="a03bf-272">RAW</span><span class="sxs-lookup"><span data-stu-id="a03bf-272">RAW</span></span> | <span data-ttu-id="a03bf-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a03bf-273">Byte[]</span></span>
<span data-ttu-id="a03bf-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="a03bf-274">RAWSTRING</span></span> | <span data-ttu-id="a03bf-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a03bf-275">Byte[]</span></span>
<span data-ttu-id="a03bf-276">STRING</span><span class="sxs-lookup"><span data-stu-id="a03bf-276">STRING</span></span> | <span data-ttu-id="a03bf-277">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-277">String</span></span>
<span data-ttu-id="a03bf-278">UNITÀ</span><span class="sxs-lookup"><span data-stu-id="a03bf-278">UNIT</span></span> | <span data-ttu-id="a03bf-279">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-279">String</span></span>
<span data-ttu-id="a03bf-280">DATS</span><span class="sxs-lookup"><span data-stu-id="a03bf-280">DATS</span></span> | <span data-ttu-id="a03bf-281">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-281">String</span></span>
<span data-ttu-id="a03bf-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="a03bf-282">NUMC</span></span> | <span data-ttu-id="a03bf-283">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-283">String</span></span>
<span data-ttu-id="a03bf-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="a03bf-284">TIMS</span></span> | <span data-ttu-id="a03bf-285">String</span><span class="sxs-lookup"><span data-stu-id="a03bf-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="a03bf-286">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="a03bf-287">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="a03bf-287">Map source to sink columns</span></span>
<span data-ttu-id="a03bf-288">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a03bf-289">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="a03bf-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="a03bf-290">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="a03bf-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a03bf-291">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="a03bf-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a03bf-292">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="a03bf-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a03bf-293">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="a03bf-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a03bf-294">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="a03bf-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a03bf-295">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a03bf-295">Performance and Tuning</span></span>
<span data-ttu-id="a03bf-296">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a03bf-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
