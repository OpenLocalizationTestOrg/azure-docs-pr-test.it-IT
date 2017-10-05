---
title: Spostare dati da Teradata usando Azure Data Factory | Documentazione Microsoft
description: Informazioni su come il connettore Teradata per il servizio Data factory consente di spostare dati dal database Teradata
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
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="6a9ef-103">Spostare i dati da Teradata utilizzando Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="6a9ef-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="6a9ef-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un database Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="6a9ef-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6a9ef-106">È possibile copiare dati da un archivio dati Teradata locale a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="6a9ef-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6a9ef-108">Data Factory supporta attualmente solo lo spostamento di dati da un archivio dati Teradata ad altri archivi dati, ma non da altri archivi dati a un archivio dati Teradata.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6a9ef-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a9ef-109">Prerequisites</span></span>
<span data-ttu-id="6a9ef-110">Data factory supporta la connessione a origini Teradata locali tramite il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="6a9ef-111">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="6a9ef-112">Il gateway è necessario anche se il database Teradata è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="6a9ef-113">È possibile installare il gateway nella stessa VM IaaS dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="6a9ef-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="6a9ef-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="6a9ef-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="6a9ef-115">Supported versions and installation</span></span>
<span data-ttu-id="6a9ef-116">Perché Gateway di gestione dati si connetta al database Teradata, è necessario installare il [provider di dati .NET per Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versione 14 o successiva nello stesso sistema di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="6a9ef-117">Sono supportate le versioni di Teradata a partire dalla 12.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6a9ef-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="6a9ef-118">Getting started</span></span>
<span data-ttu-id="6a9ef-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="6a9ef-120">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6a9ef-121">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="6a9ef-122">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6a9ef-123">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6a9ef-124">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="6a9ef-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6a9ef-125">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6a9ef-126">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6a9ef-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6a9ef-128">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6a9ef-129">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6a9ef-130">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da un archivio dati Teradata locale, vedere la sezione [Esempio JSON: Copiare dati da Teradata a BLOB di Azure](#json-example-copy-data-from-teradata-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6a9ef-131">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di un archivio dati Teradata:</span><span class="sxs-lookup"><span data-stu-id="6a9ef-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6a9ef-132">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="6a9ef-132">Linked service properties</span></span>
<span data-ttu-id="6a9ef-133">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato Teradata.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="6a9ef-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6a9ef-134">Property</span></span> | <span data-ttu-id="6a9ef-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6a9ef-135">Description</span></span> | <span data-ttu-id="6a9ef-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6a9ef-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a9ef-137">type</span><span class="sxs-lookup"><span data-stu-id="6a9ef-137">type</span></span> |<span data-ttu-id="6a9ef-138">La proprietà del tipo deve essere impostata su: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="6a9ef-139">Sì</span><span class="sxs-lookup"><span data-stu-id="6a9ef-139">Yes</span></span> |
| <span data-ttu-id="6a9ef-140">server</span><span class="sxs-lookup"><span data-stu-id="6a9ef-140">server</span></span> |<span data-ttu-id="6a9ef-141">Nome del server Teradata.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-141">Name of the Teradata server.</span></span> |<span data-ttu-id="6a9ef-142">Sì</span><span class="sxs-lookup"><span data-stu-id="6a9ef-142">Yes</span></span> |
| <span data-ttu-id="6a9ef-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6a9ef-143">authenticationType</span></span> |<span data-ttu-id="6a9ef-144">Tipo di autenticazione usato per connettersi al database Teradata.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="6a9ef-145">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="6a9ef-146">Sì</span><span class="sxs-lookup"><span data-stu-id="6a9ef-146">Yes</span></span> |
| <span data-ttu-id="6a9ef-147">username</span><span class="sxs-lookup"><span data-stu-id="6a9ef-147">username</span></span> |<span data-ttu-id="6a9ef-148">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="6a9ef-149">No</span><span class="sxs-lookup"><span data-stu-id="6a9ef-149">No</span></span> |
| <span data-ttu-id="6a9ef-150">password</span><span class="sxs-lookup"><span data-stu-id="6a9ef-150">password</span></span> |<span data-ttu-id="6a9ef-151">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6a9ef-152">No</span><span class="sxs-lookup"><span data-stu-id="6a9ef-152">No</span></span> |
| <span data-ttu-id="6a9ef-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6a9ef-153">gatewayName</span></span> |<span data-ttu-id="6a9ef-154">Nome del gateway che il servizio Data factory deve usare per connettersi al database Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="6a9ef-155">Sì</span><span class="sxs-lookup"><span data-stu-id="6a9ef-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="6a9ef-156">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="6a9ef-156">Dataset properties</span></span>
<span data-ttu-id="6a9ef-157">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6a9ef-158">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6a9ef-159">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6a9ef-160">Attualmente non sono disponibili proprietà di tipo supportate per il set di dati Teradata.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6a9ef-161">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="6a9ef-161">Copy activity properties</span></span>
<span data-ttu-id="6a9ef-162">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6a9ef-163">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="6a9ef-164">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="6a9ef-165">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6a9ef-166">Se l'origine è di tipo **RelationalSource** (che comprende Teradata), sono disponibili le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="6a9ef-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="6a9ef-167">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6a9ef-167">Property</span></span> | <span data-ttu-id="6a9ef-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6a9ef-168">Description</span></span> | <span data-ttu-id="6a9ef-169">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="6a9ef-169">Allowed values</span></span> | <span data-ttu-id="6a9ef-170">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6a9ef-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6a9ef-171">query</span><span class="sxs-lookup"><span data-stu-id="6a9ef-171">query</span></span> |<span data-ttu-id="6a9ef-172">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-172">Use the custom query to read data.</span></span> |<span data-ttu-id="6a9ef-173">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-173">SQL query string.</span></span> <span data-ttu-id="6a9ef-174">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="6a9ef-175">Sì</span><span class="sxs-lookup"><span data-stu-id="6a9ef-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="6a9ef-176">Esempio JSON: Copiare dati da Teradata a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="6a9ef-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="6a9ef-177">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6a9ef-178">Illustrano come copiare dati da Teradata in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="6a9ef-179">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="6a9ef-180">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a9ef-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="6a9ef-181">Un servizio collegato di tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="6a9ef-182">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6a9ef-183">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6a9ef-184">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6a9ef-185">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6a9ef-186">L'esempio copia i dati dai risultati della query nel database Teradata in un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="6a9ef-187">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6a9ef-188">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="6a9ef-189">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="6a9ef-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="6a9ef-190">**Servizio collegato Teradata:**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="6a9ef-191">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="6a9ef-192">**Set di dati di input Teradata:**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="6a9ef-193">L'esempio presuppone che sia stata creata una tabella "MyTable" in Teradata e che contenga una colonna denominata "timestamp" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="6a9ef-194">Impostando "external" su "true" si comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="6a9ef-195">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6a9ef-196">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6a9ef-197">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6a9ef-198">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="6a9ef-199">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="6a9ef-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6a9ef-200">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="6a9ef-201">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="6a9ef-202">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="6a9ef-203">Mapping dei tipi per Teradata</span><span class="sxs-lookup"><span data-stu-id="6a9ef-203">Type mapping for Teradata</span></span>
<span data-ttu-id="6a9ef-204">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="6a9ef-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="6a9ef-205">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="6a9ef-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6a9ef-206">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="6a9ef-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6a9ef-207">Quando si spostano i dati in Teradata vengono usati i mapping seguenti dal tipo Teradata al tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="6a9ef-208">Tipo di database Teradata</span><span class="sxs-lookup"><span data-stu-id="6a9ef-208">Teradata Database type</span></span> | <span data-ttu-id="6a9ef-209">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6a9ef-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="6a9ef-210">Char</span><span class="sxs-lookup"><span data-stu-id="6a9ef-210">Char</span></span> |<span data-ttu-id="6a9ef-211">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-211">String</span></span> |
| <span data-ttu-id="6a9ef-212">Clob</span><span class="sxs-lookup"><span data-stu-id="6a9ef-212">Clob</span></span> |<span data-ttu-id="6a9ef-213">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-213">String</span></span> |
| <span data-ttu-id="6a9ef-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="6a9ef-214">Graphic</span></span> |<span data-ttu-id="6a9ef-215">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-215">String</span></span> |
| <span data-ttu-id="6a9ef-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="6a9ef-216">VarChar</span></span> |<span data-ttu-id="6a9ef-217">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-217">String</span></span> |
| <span data-ttu-id="6a9ef-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="6a9ef-218">VarGraphic</span></span> |<span data-ttu-id="6a9ef-219">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-219">String</span></span> |
| <span data-ttu-id="6a9ef-220">BLOB</span><span class="sxs-lookup"><span data-stu-id="6a9ef-220">Blob</span></span> |<span data-ttu-id="6a9ef-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a9ef-221">Byte[]</span></span> |
| <span data-ttu-id="6a9ef-222">Byte</span><span class="sxs-lookup"><span data-stu-id="6a9ef-222">Byte</span></span> |<span data-ttu-id="6a9ef-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a9ef-223">Byte[]</span></span> |
| <span data-ttu-id="6a9ef-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="6a9ef-224">VarByte</span></span> |<span data-ttu-id="6a9ef-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a9ef-225">Byte[]</span></span> |
| <span data-ttu-id="6a9ef-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="6a9ef-226">BigInt</span></span> |<span data-ttu-id="6a9ef-227">Int64</span><span class="sxs-lookup"><span data-stu-id="6a9ef-227">Int64</span></span> |
| <span data-ttu-id="6a9ef-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="6a9ef-228">ByteInt</span></span> |<span data-ttu-id="6a9ef-229">Int16</span><span class="sxs-lookup"><span data-stu-id="6a9ef-229">Int16</span></span> |
| <span data-ttu-id="6a9ef-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a9ef-230">Decimal</span></span> |<span data-ttu-id="6a9ef-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="6a9ef-231">Decimal</span></span> |
| <span data-ttu-id="6a9ef-232">Double</span><span class="sxs-lookup"><span data-stu-id="6a9ef-232">Double</span></span> |<span data-ttu-id="6a9ef-233">Double</span><span class="sxs-lookup"><span data-stu-id="6a9ef-233">Double</span></span> |
| <span data-ttu-id="6a9ef-234">Integer</span><span class="sxs-lookup"><span data-stu-id="6a9ef-234">Integer</span></span> |<span data-ttu-id="6a9ef-235">Int32</span><span class="sxs-lookup"><span data-stu-id="6a9ef-235">Int32</span></span> |
| <span data-ttu-id="6a9ef-236">Number</span><span class="sxs-lookup"><span data-stu-id="6a9ef-236">Number</span></span> |<span data-ttu-id="6a9ef-237">Double</span><span class="sxs-lookup"><span data-stu-id="6a9ef-237">Double</span></span> |
| <span data-ttu-id="6a9ef-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="6a9ef-238">SmallInt</span></span> |<span data-ttu-id="6a9ef-239">Int16</span><span class="sxs-lookup"><span data-stu-id="6a9ef-239">Int16</span></span> |
| <span data-ttu-id="6a9ef-240">Date</span><span class="sxs-lookup"><span data-stu-id="6a9ef-240">Date</span></span> |<span data-ttu-id="6a9ef-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a9ef-241">DateTime</span></span> |
| <span data-ttu-id="6a9ef-242">Time</span><span class="sxs-lookup"><span data-stu-id="6a9ef-242">Time</span></span> |<span data-ttu-id="6a9ef-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-243">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="6a9ef-244">Time With Time Zone</span></span> |<span data-ttu-id="6a9ef-245">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-245">String</span></span> |
| <span data-ttu-id="6a9ef-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6a9ef-246">Timestamp</span></span> |<span data-ttu-id="6a9ef-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a9ef-247">DateTime</span></span> |
| <span data-ttu-id="6a9ef-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="6a9ef-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="6a9ef-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="6a9ef-249">DateTimeOffset</span></span> |
| <span data-ttu-id="6a9ef-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="6a9ef-250">Interval Day</span></span> |<span data-ttu-id="6a9ef-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-251">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-252">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="6a9ef-252">Interval Day To Hour</span></span> |<span data-ttu-id="6a9ef-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-253">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-254">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="6a9ef-254">Interval Day To Minute</span></span> |<span data-ttu-id="6a9ef-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-255">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="6a9ef-256">Interval Day To Second</span></span> |<span data-ttu-id="6a9ef-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-257">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="6a9ef-258">Interval Hour</span></span> |<span data-ttu-id="6a9ef-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-259">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-260">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="6a9ef-260">Interval Hour To Minute</span></span> |<span data-ttu-id="6a9ef-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-261">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-262">Intervallo - da ora a secondo</span><span class="sxs-lookup"><span data-stu-id="6a9ef-262">Interval Hour To Second</span></span> |<span data-ttu-id="6a9ef-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-263">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="6a9ef-264">Interval Minute</span></span> |<span data-ttu-id="6a9ef-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-265">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="6a9ef-266">Interval Minute To Second</span></span> |<span data-ttu-id="6a9ef-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-267">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="6a9ef-268">Interval Second</span></span> |<span data-ttu-id="6a9ef-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6a9ef-269">TimeSpan</span></span> |
| <span data-ttu-id="6a9ef-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="6a9ef-270">Interval Year</span></span> |<span data-ttu-id="6a9ef-271">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-271">String</span></span> |
| <span data-ttu-id="6a9ef-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="6a9ef-272">Interval Year To Month</span></span> |<span data-ttu-id="6a9ef-273">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-273">String</span></span> |
| <span data-ttu-id="6a9ef-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="6a9ef-274">Interval Month</span></span> |<span data-ttu-id="6a9ef-275">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-275">String</span></span> |
| <span data-ttu-id="6a9ef-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-276">Period(Date)</span></span> |<span data-ttu-id="6a9ef-277">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-277">String</span></span> |
| <span data-ttu-id="6a9ef-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-278">Period(Time)</span></span> |<span data-ttu-id="6a9ef-279">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-279">String</span></span> |
| <span data-ttu-id="6a9ef-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="6a9ef-281">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-281">String</span></span> |
| <span data-ttu-id="6a9ef-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-282">Period(Timestamp)</span></span> |<span data-ttu-id="6a9ef-283">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-283">String</span></span> |
| <span data-ttu-id="6a9ef-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="6a9ef-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="6a9ef-285">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-285">String</span></span> |
| <span data-ttu-id="6a9ef-286">Xml</span><span class="sxs-lookup"><span data-stu-id="6a9ef-286">Xml</span></span> |<span data-ttu-id="6a9ef-287">String</span><span class="sxs-lookup"><span data-stu-id="6a9ef-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6a9ef-288">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="6a9ef-288">Map source to sink columns</span></span>
<span data-ttu-id="6a9ef-289">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6a9ef-290">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="6a9ef-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="6a9ef-291">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6a9ef-292">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6a9ef-293">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6a9ef-294">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="6a9ef-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6a9ef-295">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6a9ef-296">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="6a9ef-296">Performance and Tuning</span></span>
<span data-ttu-id="6a9ef-297">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6a9ef-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
