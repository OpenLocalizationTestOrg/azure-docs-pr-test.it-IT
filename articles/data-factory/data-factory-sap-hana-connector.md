---
title: Spostare dati da SAP HANA usando Azure Data Factory | Microsoft Docs
description: Informazioni su come spostare dati da SAP HANA usando Azure Data Factory.
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="3016d-103">Spostare dati da SAP HANA usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3016d-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="3016d-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un database SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="3016d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="3016d-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="3016d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="3016d-106">È possibile copiare dati da un archivio dati SAP HANA locale a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="3016d-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="3016d-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3016d-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3016d-108">Data Factory supporta attualmente solo lo spostamento di dati da SAP HANA ad altri archivi dati, non da altri archivi dati a SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3016d-109">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="3016d-109">Supported versions and installation</span></span>
<span data-ttu-id="3016d-110">Questo connettore supporta qualsiasi versione del database SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="3016d-111">Supporta anche la copia di dati da modelli di informazioni HANA (ad esempio, dalle viste di analisi e calcolo) e da tabelle Riga/Colonna tramite query SQL.</span><span class="sxs-lookup"><span data-stu-id="3016d-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="3016d-112">Per abilitare la connettività all'istanza di SAP HANA, installare i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3016d-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="3016d-113">**Gateway di gestione dati**: il servizio Data Factory supporta la connessione ad archivi dati locali (incluso SAP HANA) usando un componente denominato Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3016d-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="3016d-114">Per informazioni su Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway, vedere l'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="3016d-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="3016d-115">Il gateway è necessario anche se il database SAP HANA è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="3016d-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="3016d-116">È possibile installare il gateway nella stessa VM dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="3016d-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="3016d-117">**Driver ODBC di SAP HANA** nel computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="3016d-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="3016d-118">È possibile scaricare il driver ODBC di SAP HANA dall'[area per il download di software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="3016d-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="3016d-119">Per cercare il driver, usare la parola chiave **SAP HANA CLIENT for Windows**.</span><span class="sxs-lookup"><span data-stu-id="3016d-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="3016d-120">Introduzione</span><span class="sxs-lookup"><span data-stu-id="3016d-120">Getting started</span></span>
<span data-ttu-id="3016d-121">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="3016d-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3016d-122">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="3016d-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3016d-123">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="3016d-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="3016d-124">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="3016d-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3016d-125">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="3016d-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3016d-126">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="3016d-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3016d-127">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="3016d-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="3016d-128">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="3016d-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="3016d-129">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="3016d-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3016d-130">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3016d-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3016d-131">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3016d-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3016d-132">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da un SAP HANA locale, vedere la sezione [Esempio JSON: Copiare dati da SAP HANA a BLOB di Azure](#json-example-copy-data-from-sap-hana-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3016d-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3016d-133">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di un archivio dati SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="3016d-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3016d-134">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="3016d-134">Linked service properties</span></span>
<span data-ttu-id="3016d-135">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="3016d-136">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3016d-136">Property</span></span> | <span data-ttu-id="3016d-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3016d-137">Description</span></span> | <span data-ttu-id="3016d-138">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="3016d-138">Allowed values</span></span> | <span data-ttu-id="3016d-139">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="3016d-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3016d-140">server</span><span class="sxs-lookup"><span data-stu-id="3016d-140">server</span></span> | <span data-ttu-id="3016d-141">Nome del server in cui si trova l'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="3016d-142">Se il server usa una porta personalizzata, specificare `server:port`.</span><span class="sxs-lookup"><span data-stu-id="3016d-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="3016d-143">string</span><span class="sxs-lookup"><span data-stu-id="3016d-143">string</span></span> | <span data-ttu-id="3016d-144">Sì</span><span class="sxs-lookup"><span data-stu-id="3016d-144">Yes</span></span>
<span data-ttu-id="3016d-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3016d-145">authenticationType</span></span> | <span data-ttu-id="3016d-146">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3016d-146">Type of authentication.</span></span> | <span data-ttu-id="3016d-147">string.</span><span class="sxs-lookup"><span data-stu-id="3016d-147">string.</span></span> <span data-ttu-id="3016d-148">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="3016d-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="3016d-149">Sì</span><span class="sxs-lookup"><span data-stu-id="3016d-149">Yes</span></span> 
<span data-ttu-id="3016d-150">username</span><span class="sxs-lookup"><span data-stu-id="3016d-150">username</span></span> | <span data-ttu-id="3016d-151">Nome dell'utente che ha accesso al server SAP</span><span class="sxs-lookup"><span data-stu-id="3016d-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="3016d-152">string</span><span class="sxs-lookup"><span data-stu-id="3016d-152">string</span></span> | <span data-ttu-id="3016d-153">Sì</span><span class="sxs-lookup"><span data-stu-id="3016d-153">Yes</span></span>
<span data-ttu-id="3016d-154">password</span><span class="sxs-lookup"><span data-stu-id="3016d-154">password</span></span> | <span data-ttu-id="3016d-155">Password per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3016d-155">Password for the user.</span></span> | <span data-ttu-id="3016d-156">string</span><span class="sxs-lookup"><span data-stu-id="3016d-156">string</span></span> | <span data-ttu-id="3016d-157">Sì</span><span class="sxs-lookup"><span data-stu-id="3016d-157">Yes</span></span>
<span data-ttu-id="3016d-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3016d-158">gatewayName</span></span> | <span data-ttu-id="3016d-159">Nome del gateway che il servizio Data factory deve usare per connettersi all'istanza di SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="3016d-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="3016d-160">string</span><span class="sxs-lookup"><span data-stu-id="3016d-160">string</span></span> | <span data-ttu-id="3016d-161">Sì</span><span class="sxs-lookup"><span data-stu-id="3016d-161">Yes</span></span>
<span data-ttu-id="3016d-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3016d-162">encryptedCredential</span></span> | <span data-ttu-id="3016d-163">Stringa di credenziali crittografata.</span><span class="sxs-lookup"><span data-stu-id="3016d-163">The encrypted credential string.</span></span> | <span data-ttu-id="3016d-164">string</span><span class="sxs-lookup"><span data-stu-id="3016d-164">string</span></span> | <span data-ttu-id="3016d-165">No</span><span class="sxs-lookup"><span data-stu-id="3016d-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="3016d-166">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="3016d-166">Dataset properties</span></span>
<span data-ttu-id="3016d-167">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3016d-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3016d-168">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="3016d-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3016d-169">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="3016d-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3016d-170">Il set di dati SAP HANA di tipo **RelationalTable** non supporta alcuna proprietà specifica del tipo.</span><span class="sxs-lookup"><span data-stu-id="3016d-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="3016d-171">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="3016d-171">Copy activity properties</span></span>
<span data-ttu-id="3016d-172">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3016d-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3016d-173">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="3016d-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="3016d-174">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="3016d-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="3016d-175">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="3016d-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="3016d-176">Se l'origine nell'attività di copia è di tipo **RelationalSource** (che include SAP HANA), nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="3016d-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3016d-177">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3016d-177">Property</span></span> | <span data-ttu-id="3016d-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3016d-178">Description</span></span> | <span data-ttu-id="3016d-179">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="3016d-179">Allowed values</span></span> | <span data-ttu-id="3016d-180">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3016d-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3016d-181">query</span><span class="sxs-lookup"><span data-stu-id="3016d-181">query</span></span> | <span data-ttu-id="3016d-182">Specifica la query SQL che consente di leggere i dati dall'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="3016d-183">Query SQL.</span><span class="sxs-lookup"><span data-stu-id="3016d-183">SQL query.</span></span> | <span data-ttu-id="3016d-184">Sì</span><span class="sxs-lookup"><span data-stu-id="3016d-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="3016d-185">Esempio JSON: Copiare dati da SAP HANA a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="3016d-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="3016d-186">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline tramite il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3016d-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3016d-187">Questo esempio illustra come copiare dati da un database SAP HANA locale a un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="3016d-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="3016d-188">I dati possono tuttavia essere copiati **direttamente** in qualsiasi sink elencato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3016d-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3016d-189">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="3016d-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="3016d-190">Non include istruzioni dettagliate per la creazione della data factory.</span><span class="sxs-lookup"><span data-stu-id="3016d-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="3016d-191">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="3016d-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3016d-192">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="3016d-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3016d-193">Un servizio collegato di tipo [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3016d-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="3016d-194">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3016d-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3016d-195">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3016d-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3016d-196">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3016d-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3016d-197">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3016d-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3016d-198">Nell'esempio i dati vengono copiati da un'istanza di SAP HANA a un BLOB di Azure a intervalli orari.</span><span class="sxs-lookup"><span data-stu-id="3016d-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="3016d-199">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="3016d-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3016d-200">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3016d-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="3016d-201">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="3016d-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="3016d-202">Servizio collegato SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3016d-202">SAP HANA linked service</span></span>
<span data-ttu-id="3016d-203">Questo servizio collegato collega l'istanza di SAP HANA alla data factory.</span><span class="sxs-lookup"><span data-stu-id="3016d-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="3016d-204">La proprietà type è impostata su **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="3016d-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="3016d-205">La sezione typeProperties fornisce informazioni di connessione per l'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="3016d-206">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3016d-206">Azure Storage linked service</span></span>
<span data-ttu-id="3016d-207">Questo servizio collegato collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="3016d-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="3016d-208">La proprietà type è impostata su **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="3016d-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="3016d-209">La sezione typeProperties fornisce informazioni di connessione per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3016d-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="3016d-210">Set di dati input di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3016d-210">SAP HANA input dataset</span></span>

<span data-ttu-id="3016d-211">Questo set di dati definisce il set di dati di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="3016d-212">Per il set di dati Data Factory il tipo deve essere impostato su **RelationalTable**,</span><span class="sxs-lookup"><span data-stu-id="3016d-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="3016d-213">mentre per il set di dati SAP HANA non è attualmente necessario specificare alcuna proprietà relativa al tipo.</span><span class="sxs-lookup"><span data-stu-id="3016d-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="3016d-214">La query presente nella definizione dell'attività di copia specifica i dati da leggere dall'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="3016d-215">Impostando la proprietà esterna su true si comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="3016d-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="3016d-216">Le proprietà di frequenza e intervallo definiscono la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="3016d-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="3016d-217">In questo caso, i dati vengono letti dall'istanza di SAP HANA ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3016d-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3016d-218">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="3016d-218">Azure Blob output dataset</span></span>
<span data-ttu-id="3016d-219">Questo set di dati definisce il set di dati di output di BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="3016d-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="3016d-220">La proprietà type è impostata su AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="3016d-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="3016d-221">La sezione typeProperties specifica dove devono essere archiviati i dati copiati dall'istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3016d-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="3016d-222">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="3016d-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3016d-223">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="3016d-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3016d-224">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="3016d-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="3016d-225">Pipeline con attività di copia</span><span class="sxs-lookup"><span data-stu-id="3016d-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="3016d-226">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3016d-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3016d-227">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** (per l'origine SAP HANA) e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3016d-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="3016d-228">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="3016d-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="3016d-229">Mapping dei tipi per SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3016d-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="3016d-230">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="3016d-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="3016d-231">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="3016d-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3016d-232">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="3016d-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3016d-233">Quando si spostano dati da SAP HANA, vengono usati i mapping seguenti tra i tipi SAP HANA e i tipi .NET.</span><span class="sxs-lookup"><span data-stu-id="3016d-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="3016d-234">Tipo SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3016d-234">SAP HANA Type</span></span> | <span data-ttu-id="3016d-235">Tipo basato su .Net</span><span class="sxs-lookup"><span data-stu-id="3016d-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="3016d-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="3016d-236">TINYINT</span></span> | <span data-ttu-id="3016d-237">Byte</span><span class="sxs-lookup"><span data-stu-id="3016d-237">Byte</span></span>
<span data-ttu-id="3016d-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="3016d-238">SMALLINT</span></span> | <span data-ttu-id="3016d-239">Int16</span><span class="sxs-lookup"><span data-stu-id="3016d-239">Int16</span></span>
<span data-ttu-id="3016d-240">INT</span><span class="sxs-lookup"><span data-stu-id="3016d-240">INT</span></span> | <span data-ttu-id="3016d-241">Int32</span><span class="sxs-lookup"><span data-stu-id="3016d-241">Int32</span></span>
<span data-ttu-id="3016d-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="3016d-242">BIGINT</span></span> | <span data-ttu-id="3016d-243">Int64</span><span class="sxs-lookup"><span data-stu-id="3016d-243">Int64</span></span>
<span data-ttu-id="3016d-244">REAL</span><span class="sxs-lookup"><span data-stu-id="3016d-244">REAL</span></span> | <span data-ttu-id="3016d-245">Single</span><span class="sxs-lookup"><span data-stu-id="3016d-245">Single</span></span>
<span data-ttu-id="3016d-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="3016d-246">DOUBLE</span></span> | <span data-ttu-id="3016d-247">Single</span><span class="sxs-lookup"><span data-stu-id="3016d-247">Single</span></span>
<span data-ttu-id="3016d-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="3016d-248">DECIMAL</span></span> | <span data-ttu-id="3016d-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="3016d-249">Decimal</span></span>
<span data-ttu-id="3016d-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="3016d-250">BOOLEAN</span></span> | <span data-ttu-id="3016d-251">Byte</span><span class="sxs-lookup"><span data-stu-id="3016d-251">Byte</span></span>
<span data-ttu-id="3016d-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="3016d-252">VARCHAR</span></span> | <span data-ttu-id="3016d-253">String</span><span class="sxs-lookup"><span data-stu-id="3016d-253">String</span></span>
<span data-ttu-id="3016d-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="3016d-254">NVARCHAR</span></span> | <span data-ttu-id="3016d-255">String</span><span class="sxs-lookup"><span data-stu-id="3016d-255">String</span></span>
<span data-ttu-id="3016d-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="3016d-256">CLOB</span></span> | <span data-ttu-id="3016d-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3016d-257">Byte[]</span></span>
<span data-ttu-id="3016d-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="3016d-258">ALPHANUM</span></span> | <span data-ttu-id="3016d-259">String</span><span class="sxs-lookup"><span data-stu-id="3016d-259">String</span></span>
<span data-ttu-id="3016d-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="3016d-260">BLOB</span></span> | <span data-ttu-id="3016d-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3016d-261">Byte[]</span></span>
<span data-ttu-id="3016d-262">DATE</span><span class="sxs-lookup"><span data-stu-id="3016d-262">DATE</span></span> | <span data-ttu-id="3016d-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="3016d-263">DateTime</span></span>
<span data-ttu-id="3016d-264">TIME</span><span class="sxs-lookup"><span data-stu-id="3016d-264">TIME</span></span> | <span data-ttu-id="3016d-265">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="3016d-265">TimeSpan</span></span>
<span data-ttu-id="3016d-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="3016d-266">TIMESTAMP</span></span> | <span data-ttu-id="3016d-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="3016d-267">DateTime</span></span>
<span data-ttu-id="3016d-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="3016d-268">SECONDDATE</span></span> | <span data-ttu-id="3016d-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="3016d-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="3016d-270">Limitazioni note</span><span class="sxs-lookup"><span data-stu-id="3016d-270">Known limitations</span></span>
<span data-ttu-id="3016d-271">Quando si copiano dati da SAP HANA, è necessario tenere conto di alcune limitazioni:</span><span class="sxs-lookup"><span data-stu-id="3016d-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="3016d-272">Le stringhe NVARCHAR vengono troncate alla lunghezza massima di 4000 caratteri Unicode</span><span class="sxs-lookup"><span data-stu-id="3016d-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="3016d-273">SMALLDECIMAL non è supportato</span><span class="sxs-lookup"><span data-stu-id="3016d-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="3016d-274">VARBINARY non è supportato</span><span class="sxs-lookup"><span data-stu-id="3016d-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="3016d-275">Le date valide sono tra comprese tra il 30/12/1899 e il 31/12/9999</span><span class="sxs-lookup"><span data-stu-id="3016d-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="3016d-276">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="3016d-276">Map source to sink columns</span></span>
<span data-ttu-id="3016d-277">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3016d-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3016d-278">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="3016d-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="3016d-279">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="3016d-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3016d-280">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="3016d-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3016d-281">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="3016d-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3016d-282">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="3016d-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3016d-283">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="3016d-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3016d-284">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="3016d-284">Performance and Tuning</span></span>
<span data-ttu-id="3016d-285">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="3016d-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
