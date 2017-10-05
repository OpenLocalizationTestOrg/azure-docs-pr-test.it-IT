---
title: Spostare dati da MySQL usando Azure Data Factory | Documentazione Microsoft
description: Informazioni su come spostare i dati dal database di MySQL mediante Data factory di Azure.
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
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="31889-103">Spostare i dati da MySQL mediante Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="31889-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="31889-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un database MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="31889-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="31889-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="31889-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="31889-106">È possibile copiare dati da un archivio dati MySQL locale a qualsiasi archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="31889-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="31889-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="31889-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="31889-108">Data Factory supporta attualmente solo lo spostamento dei dati da un archivio dati MySQL ad altri archivi dati, ma non da altri archivi dati a un archivio dati MySQL.</span><span class="sxs-lookup"><span data-stu-id="31889-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31889-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="31889-109">Prerequisites</span></span>
<span data-ttu-id="31889-110">Data factory supporta la connessione a origini MySQL locali tramite il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="31889-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="31889-111">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="31889-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="31889-112">Il gateway è necessario anche se il database MySQL è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="31889-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="31889-113">È possibile installare il gateway nella stessa VM dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="31889-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="31889-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="31889-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="31889-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="31889-115">Supported versions and installation</span></span>
<span data-ttu-id="31889-116">Perché Gateway di gestione dati si connetta al database MySQL, è necessario installare il [connettore MySQL/Net per Microsoft Windows](https://dev.mysql.com/downloads/connector/net/), versione 6.6.5 o una versione successiva, nello stesso sistema di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="31889-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="31889-117">Sono supportate le versioni di MySQL a partire dalla 5.1.</span><span class="sxs-lookup"><span data-stu-id="31889-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="31889-118">Se si ottiene l'errore "Autenticazione non riuscita. La parte remota ha chiuso il flusso di trasporto.", è consigliabile aggiornare il connettore MySQL/Net alla versione successiva.</span><span class="sxs-lookup"><span data-stu-id="31889-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="31889-119">introduttiva</span><span class="sxs-lookup"><span data-stu-id="31889-119">Getting started</span></span>
<span data-ttu-id="31889-120">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="31889-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="31889-121">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="31889-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="31889-122">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="31889-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="31889-123">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="31889-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="31889-124">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="31889-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="31889-125">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="31889-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="31889-126">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="31889-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="31889-127">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="31889-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="31889-128">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="31889-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="31889-129">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="31889-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="31889-130">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="31889-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="31889-131">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da un archivio dati MySQL locale, vedere la sezione [Esempio JSON: Copiare dati da MySQL a BLOB di Azure](#json-example-copy-data-from-mysql-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="31889-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="31889-132">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un archivio dati MySQL:</span><span class="sxs-lookup"><span data-stu-id="31889-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="31889-133">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="31889-133">Linked service properties</span></span>
<span data-ttu-id="31889-134">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato MySQL.</span><span class="sxs-lookup"><span data-stu-id="31889-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="31889-135">Proprietà</span><span class="sxs-lookup"><span data-stu-id="31889-135">Property</span></span> | <span data-ttu-id="31889-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31889-136">Description</span></span> | <span data-ttu-id="31889-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="31889-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31889-138">type</span><span class="sxs-lookup"><span data-stu-id="31889-138">type</span></span> |<span data-ttu-id="31889-139">La proprietà type deve essere impostata su: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="31889-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="31889-140">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-140">Yes</span></span> |
| <span data-ttu-id="31889-141">server</span><span class="sxs-lookup"><span data-stu-id="31889-141">server</span></span> |<span data-ttu-id="31889-142">Nome del server MySQL.</span><span class="sxs-lookup"><span data-stu-id="31889-142">Name of the MySQL server.</span></span> |<span data-ttu-id="31889-143">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-143">Yes</span></span> |
| <span data-ttu-id="31889-144">database</span><span class="sxs-lookup"><span data-stu-id="31889-144">database</span></span> |<span data-ttu-id="31889-145">Nome del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="31889-145">Name of the MySQL database.</span></span> |<span data-ttu-id="31889-146">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-146">Yes</span></span> |
| <span data-ttu-id="31889-147">schema</span><span class="sxs-lookup"><span data-stu-id="31889-147">schema</span></span> |<span data-ttu-id="31889-148">Nome dello schema nel database.</span><span class="sxs-lookup"><span data-stu-id="31889-148">Name of the schema in the database.</span></span> |<span data-ttu-id="31889-149">No</span><span class="sxs-lookup"><span data-stu-id="31889-149">No</span></span> |
| <span data-ttu-id="31889-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="31889-150">authenticationType</span></span> |<span data-ttu-id="31889-151">Tipo di autenticazione usato per connettersi al database MySQL.</span><span class="sxs-lookup"><span data-stu-id="31889-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="31889-152">I valori possibili sono:`Basic`.</span><span class="sxs-lookup"><span data-stu-id="31889-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="31889-153">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-153">Yes</span></span> |
| <span data-ttu-id="31889-154">username</span><span class="sxs-lookup"><span data-stu-id="31889-154">username</span></span> |<span data-ttu-id="31889-155">Specificare nome utente per la connessione al database MySQL.</span><span class="sxs-lookup"><span data-stu-id="31889-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="31889-156">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-156">Yes</span></span> |
| <span data-ttu-id="31889-157">password</span><span class="sxs-lookup"><span data-stu-id="31889-157">password</span></span> |<span data-ttu-id="31889-158">Specificare la password per l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="31889-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="31889-159">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-159">Yes</span></span> |
| <span data-ttu-id="31889-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="31889-160">gatewayName</span></span> |<span data-ttu-id="31889-161">Nome del gateway che il servizio Data factory deve usare per connettersi al database MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="31889-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="31889-162">Sì</span><span class="sxs-lookup"><span data-stu-id="31889-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="31889-163">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="31889-163">Dataset properties</span></span>
<span data-ttu-id="31889-164">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="31889-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="31889-165">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="31889-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="31889-166">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="31889-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="31889-167">La sezione typeProperties per il set di dati di tipo **RelationalTable** (che comprende il set di dati MySQL) presenta le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="31889-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="31889-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="31889-168">Property</span></span> | <span data-ttu-id="31889-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31889-169">Description</span></span> | <span data-ttu-id="31889-170">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="31889-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31889-171">tableName</span><span class="sxs-lookup"><span data-stu-id="31889-171">tableName</span></span> |<span data-ttu-id="31889-172">Nome della tabella nell'istanza del database MySQL a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="31889-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="31889-173">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="31889-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="31889-174">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="31889-174">Copy activity properties</span></span>
<span data-ttu-id="31889-175">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="31889-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="31889-176">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="31889-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="31889-177">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="31889-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="31889-178">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="31889-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="31889-179">Se l'origine nell'attività di copia è di tipo **RelationalSource** (che comprende MySQL), sono disponibili le proprietà seguenti nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="31889-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="31889-180">Proprietà</span><span class="sxs-lookup"><span data-stu-id="31889-180">Property</span></span> | <span data-ttu-id="31889-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31889-181">Description</span></span> | <span data-ttu-id="31889-182">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="31889-182">Allowed values</span></span> | <span data-ttu-id="31889-183">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="31889-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31889-184">query</span><span class="sxs-lookup"><span data-stu-id="31889-184">query</span></span> |<span data-ttu-id="31889-185">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="31889-185">Use the custom query to read data.</span></span> |<span data-ttu-id="31889-186">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="31889-186">SQL query string.</span></span> <span data-ttu-id="31889-187">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="31889-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="31889-188">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="31889-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="31889-189">Esempio JSON: Copiare dati da MySQL a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="31889-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="31889-190">Questo esempio fornisce le definizioni JSON di esempio da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="31889-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="31889-191">Illustra come copiare dati da un database MySQL locale a una istanza di Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="31889-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="31889-192">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="31889-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31889-193">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="31889-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="31889-194">Non include istruzioni dettagliate per la creazione della data factory.</span><span class="sxs-lookup"><span data-stu-id="31889-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="31889-195">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="31889-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="31889-196">L'esempio include le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="31889-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="31889-197">Un servizio collegato di tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="31889-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="31889-198">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="31889-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="31889-199">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="31889-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="31889-200">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="31889-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="31889-201">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="31889-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="31889-202">L'esempio copia i dati dai risultati della query nel database MySQL in un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="31889-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="31889-203">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="31889-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="31889-204">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="31889-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="31889-205">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="31889-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="31889-206">**Servizio collegato MySQL**</span><span class="sxs-lookup"><span data-stu-id="31889-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="31889-207">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="31889-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="31889-208">**Set di dati di input MySQL**</span><span class="sxs-lookup"><span data-stu-id="31889-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="31889-209">L'esempio presuppone che sia stata creata una tabella "MyTable" in MySQL e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="31889-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="31889-210">Impostando "external" su "true" si comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="31889-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="31889-211">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="31889-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="31889-212">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="31889-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="31889-213">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="31889-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="31889-214">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="31889-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="31889-215">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="31889-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="31889-216">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="31889-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="31889-217">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="31889-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="31889-218">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="31889-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="31889-219">Mapping dei tipi per MySQL</span><span class="sxs-lookup"><span data-stu-id="31889-219">Type mapping for MySQL</span></span>
<span data-ttu-id="31889-220">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="31889-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="31889-221">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="31889-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="31889-222">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="31889-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="31889-223">Quando si spostano i dati in MySQL vengono usati i mapping seguenti dal tipo MySQL al tipo .NET.</span><span class="sxs-lookup"><span data-stu-id="31889-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="31889-224">Tipo di database MySQL</span><span class="sxs-lookup"><span data-stu-id="31889-224">MySQL Database type</span></span> | <span data-ttu-id="31889-225">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="31889-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="31889-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="31889-226">bigint unsigned</span></span> |<span data-ttu-id="31889-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="31889-227">Decimal</span></span> |
| <span data-ttu-id="31889-228">bigint</span><span class="sxs-lookup"><span data-stu-id="31889-228">bigint</span></span> |<span data-ttu-id="31889-229">Int64</span><span class="sxs-lookup"><span data-stu-id="31889-229">Int64</span></span> |
| <span data-ttu-id="31889-230">Bit</span><span class="sxs-lookup"><span data-stu-id="31889-230">bit</span></span> |<span data-ttu-id="31889-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="31889-231">Decimal</span></span> |
| <span data-ttu-id="31889-232">BLOB</span><span class="sxs-lookup"><span data-stu-id="31889-232">blob</span></span> |<span data-ttu-id="31889-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="31889-233">Byte[]</span></span> |
| <span data-ttu-id="31889-234">bool</span><span class="sxs-lookup"><span data-stu-id="31889-234">bool</span></span> |<span data-ttu-id="31889-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="31889-235">Boolean</span></span> |
| <span data-ttu-id="31889-236">char</span><span class="sxs-lookup"><span data-stu-id="31889-236">char</span></span> |<span data-ttu-id="31889-237">String</span><span class="sxs-lookup"><span data-stu-id="31889-237">String</span></span> |
| <span data-ttu-id="31889-238">date</span><span class="sxs-lookup"><span data-stu-id="31889-238">date</span></span> |<span data-ttu-id="31889-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="31889-239">Datetime</span></span> |
| <span data-ttu-id="31889-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="31889-240">datetime</span></span> |<span data-ttu-id="31889-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="31889-241">Datetime</span></span> |
| <span data-ttu-id="31889-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="31889-242">decimal</span></span> |<span data-ttu-id="31889-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="31889-243">Decimal</span></span> |
| <span data-ttu-id="31889-244">double precision</span><span class="sxs-lookup"><span data-stu-id="31889-244">double precision</span></span> |<span data-ttu-id="31889-245">Double</span><span class="sxs-lookup"><span data-stu-id="31889-245">Double</span></span> |
| <span data-ttu-id="31889-246">Double</span><span class="sxs-lookup"><span data-stu-id="31889-246">double</span></span> |<span data-ttu-id="31889-247">Double</span><span class="sxs-lookup"><span data-stu-id="31889-247">Double</span></span> |
| <span data-ttu-id="31889-248">enum</span><span class="sxs-lookup"><span data-stu-id="31889-248">enum</span></span> |<span data-ttu-id="31889-249">String</span><span class="sxs-lookup"><span data-stu-id="31889-249">String</span></span> |
| <span data-ttu-id="31889-250">float</span><span class="sxs-lookup"><span data-stu-id="31889-250">float</span></span> |<span data-ttu-id="31889-251">Single</span><span class="sxs-lookup"><span data-stu-id="31889-251">Single</span></span> |
| <span data-ttu-id="31889-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="31889-252">int unsigned</span></span> |<span data-ttu-id="31889-253">Int64</span><span class="sxs-lookup"><span data-stu-id="31889-253">Int64</span></span> |
| <span data-ttu-id="31889-254">int</span><span class="sxs-lookup"><span data-stu-id="31889-254">int</span></span> |<span data-ttu-id="31889-255">Int32</span><span class="sxs-lookup"><span data-stu-id="31889-255">Int32</span></span> |
| <span data-ttu-id="31889-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="31889-256">integer unsigned</span></span> |<span data-ttu-id="31889-257">Int64</span><span class="sxs-lookup"><span data-stu-id="31889-257">Int64</span></span> |
| <span data-ttu-id="31889-258">integer</span><span class="sxs-lookup"><span data-stu-id="31889-258">integer</span></span> |<span data-ttu-id="31889-259">Int32</span><span class="sxs-lookup"><span data-stu-id="31889-259">Int32</span></span> |
| <span data-ttu-id="31889-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="31889-260">long varbinary</span></span> |<span data-ttu-id="31889-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="31889-261">Byte[]</span></span> |
| <span data-ttu-id="31889-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="31889-262">long varchar</span></span> |<span data-ttu-id="31889-263">String</span><span class="sxs-lookup"><span data-stu-id="31889-263">String</span></span> |
| <span data-ttu-id="31889-264">longblob</span><span class="sxs-lookup"><span data-stu-id="31889-264">longblob</span></span> |<span data-ttu-id="31889-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="31889-265">Byte[]</span></span> |
| <span data-ttu-id="31889-266">longtext</span><span class="sxs-lookup"><span data-stu-id="31889-266">longtext</span></span> |<span data-ttu-id="31889-267">String</span><span class="sxs-lookup"><span data-stu-id="31889-267">String</span></span> |
| <span data-ttu-id="31889-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="31889-268">mediumblob</span></span> |<span data-ttu-id="31889-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="31889-269">Byte[]</span></span> |
| <span data-ttu-id="31889-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="31889-270">mediumint unsigned</span></span> |<span data-ttu-id="31889-271">Int64</span><span class="sxs-lookup"><span data-stu-id="31889-271">Int64</span></span> |
| <span data-ttu-id="31889-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="31889-272">mediumint</span></span> |<span data-ttu-id="31889-273">Int32</span><span class="sxs-lookup"><span data-stu-id="31889-273">Int32</span></span> |
| <span data-ttu-id="31889-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="31889-274">mediumtext</span></span> |<span data-ttu-id="31889-275">String</span><span class="sxs-lookup"><span data-stu-id="31889-275">String</span></span> |
| <span data-ttu-id="31889-276">numeric</span><span class="sxs-lookup"><span data-stu-id="31889-276">numeric</span></span> |<span data-ttu-id="31889-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="31889-277">Decimal</span></span> |
| <span data-ttu-id="31889-278">real</span><span class="sxs-lookup"><span data-stu-id="31889-278">real</span></span> |<span data-ttu-id="31889-279">Double</span><span class="sxs-lookup"><span data-stu-id="31889-279">Double</span></span> |
| <span data-ttu-id="31889-280">set</span><span class="sxs-lookup"><span data-stu-id="31889-280">set</span></span> |<span data-ttu-id="31889-281">String</span><span class="sxs-lookup"><span data-stu-id="31889-281">String</span></span> |
| <span data-ttu-id="31889-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="31889-282">smallint unsigned</span></span> |<span data-ttu-id="31889-283">Int32</span><span class="sxs-lookup"><span data-stu-id="31889-283">Int32</span></span> |
| <span data-ttu-id="31889-284">smallint</span><span class="sxs-lookup"><span data-stu-id="31889-284">smallint</span></span> |<span data-ttu-id="31889-285">Int16</span><span class="sxs-lookup"><span data-stu-id="31889-285">Int16</span></span> |
| <span data-ttu-id="31889-286">text</span><span class="sxs-lookup"><span data-stu-id="31889-286">text</span></span> |<span data-ttu-id="31889-287">String</span><span class="sxs-lookup"><span data-stu-id="31889-287">String</span></span> |
| <span data-ttu-id="31889-288">time</span><span class="sxs-lookup"><span data-stu-id="31889-288">time</span></span> |<span data-ttu-id="31889-289">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="31889-289">TimeSpan</span></span> |
| <span data-ttu-id="31889-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="31889-290">timestamp</span></span> |<span data-ttu-id="31889-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="31889-291">Datetime</span></span> |
| <span data-ttu-id="31889-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="31889-292">tinyblob</span></span> |<span data-ttu-id="31889-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="31889-293">Byte[]</span></span> |
| <span data-ttu-id="31889-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="31889-294">tinyint unsigned</span></span> |<span data-ttu-id="31889-295">Int16</span><span class="sxs-lookup"><span data-stu-id="31889-295">Int16</span></span> |
| <span data-ttu-id="31889-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="31889-296">tinyint</span></span> |<span data-ttu-id="31889-297">Int16</span><span class="sxs-lookup"><span data-stu-id="31889-297">Int16</span></span> |
| <span data-ttu-id="31889-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="31889-298">tinytext</span></span> |<span data-ttu-id="31889-299">String</span><span class="sxs-lookup"><span data-stu-id="31889-299">String</span></span> |
| <span data-ttu-id="31889-300">varchar</span><span class="sxs-lookup"><span data-stu-id="31889-300">varchar</span></span> |<span data-ttu-id="31889-301">String</span><span class="sxs-lookup"><span data-stu-id="31889-301">String</span></span> |
| <span data-ttu-id="31889-302">year</span><span class="sxs-lookup"><span data-stu-id="31889-302">year</span></span> |<span data-ttu-id="31889-303">int</span><span class="sxs-lookup"><span data-stu-id="31889-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="31889-304">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="31889-304">Map source to sink columns</span></span>
<span data-ttu-id="31889-305">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="31889-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="31889-306">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="31889-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="31889-307">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="31889-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="31889-308">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="31889-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="31889-309">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="31889-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="31889-310">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="31889-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="31889-311">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="31889-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="31889-312">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="31889-312">Performance and Tuning</span></span>
<span data-ttu-id="31889-313">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="31889-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
