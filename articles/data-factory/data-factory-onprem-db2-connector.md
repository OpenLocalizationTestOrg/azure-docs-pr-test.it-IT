---
title: Spostare dati da DB2 mediante Azure Data Factory | Microsoft Docs
description: "Informazioni su come spostare dati da un database DB2 locale mediante l'attività di copia di Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="54fca-103">Spostare dati da DB2 mediante l'attività di copia di Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="54fca-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="54fca-104">Questo articolo descrive come usare l'attività di copia in Azure Data Factory per copiare dati da un database DB2 locale a un altro archivio dati.</span><span class="sxs-lookup"><span data-stu-id="54fca-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="54fca-105">È possibile copiare dati in qualsiasi archivio che sia elencato come un sink supportato nell'articolo sulle [attività di spostamento dati di Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="54fca-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="54fca-106">Questo argomento si basa sull'articolo relativo a Data Factory, che offre una panoramica dello spostamento dei dati mediante l'attività di copia ed elenca le combinazioni di archivi dati supportati.</span><span class="sxs-lookup"><span data-stu-id="54fca-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="54fca-107">Data Factory consente attualmente solo lo spostamento dei dati da un database DB2 a un [archivio dati sink supportato](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="54fca-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="54fca-108">Lo spostamento dei dati da altri archivi dati in un database DB2 non è consentito.</span><span class="sxs-lookup"><span data-stu-id="54fca-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54fca-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="54fca-109">Prerequisites</span></span>
<span data-ttu-id="54fca-110">Data Factory supporta la connessione a database DB2 locali mediante il [gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="54fca-111">Per istruzioni passo per passo su come configurare il gateway di una pipeline di dati per spostare i dati, vedere [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="54fca-112">Un gateway è necessario anche se il DB2 è ospitato in una VM IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="54fca-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="54fca-113">È possibile installare il gateway nella stessa VM IaaS dell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="54fca-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="54fca-114">Se il gateway può connettersi al database, è possibile installare il gateway su una VM diversa.</span><span class="sxs-lookup"><span data-stu-id="54fca-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="54fca-115">Il gateway di gestione dati offre un driver DB2 integrato, perciò non è necessario installare manualmente un driver per copiare dati da DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="54fca-116">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere l'articolo [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="54fca-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="54fca-117">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="54fca-117">Supported versions</span></span>
<span data-ttu-id="54fca-118">Il connettore Data Factory DB2 supporta le piattaforme e le versioni di IBM DB2 seguenti con DRDA (Distributed Relational Database Architecture) SQL Access Manager versione 9, 10 e 11:</span><span class="sxs-lookup"><span data-stu-id="54fca-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="54fca-119">IBM DB2 per z/OS versione 11.1</span><span class="sxs-lookup"><span data-stu-id="54fca-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="54fca-120">IBM DB2 per z/OS versione 10.1</span><span class="sxs-lookup"><span data-stu-id="54fca-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="54fca-121">IBM DB2 per i (AS400) versione 7.2</span><span class="sxs-lookup"><span data-stu-id="54fca-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="54fca-122">IBM DB2 per i (AS400) versione 7.1</span><span class="sxs-lookup"><span data-stu-id="54fca-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="54fca-123">IBM DB2 per Linux, UNIX e Windows (LUW) versione 11</span><span class="sxs-lookup"><span data-stu-id="54fca-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="54fca-124">IBM DB2 per LUW versione 10.5</span><span class="sxs-lookup"><span data-stu-id="54fca-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="54fca-125">IBM DB2 per LUW versione 10.1</span><span class="sxs-lookup"><span data-stu-id="54fca-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="54fca-126">Se si riceve il messaggio d'errore "Non è stato trovato il pacchetto corrispondente a una richiesta di esecuzione dell'istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="54fca-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="54fca-127">SQLSTATE=51002 SQLCODE=-805", il motivo è che non viene creato un pacchetto necessario per un utente normale nel sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="54fca-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="54fca-128">Per risolvere il problema seguire queste istruzioni per il tipo di server DB2 in uso:</span><span class="sxs-lookup"><span data-stu-id="54fca-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="54fca-129">DB2 per i (AS400): consente all'utente esperto di creare una raccolta per l'utente normale prima di eseguire l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="54fca-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="54fca-130">Per creare la raccolta usare il comando: `create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="54fca-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="54fca-131">DB2 per z/OS o LUW: usare un account con privilegi elevati, ovvero utente esperto o amministratore con autorità di pacchetto e autorizzazioni BIND, BINDADD, GRANT EXECUTE TO PUBLIC, per eseguire l'attività di copia una volta.</span><span class="sxs-lookup"><span data-stu-id="54fca-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="54fca-132">Il pacchetto necessario viene creato automaticamente durante la copia.</span><span class="sxs-lookup"><span data-stu-id="54fca-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="54fca-133">In seguito è possibile tornare a essere un utente normale per le successive esecuzioni delle operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="54fca-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="54fca-134">introduttiva</span><span class="sxs-lookup"><span data-stu-id="54fca-134">Getting started</span></span>
<span data-ttu-id="54fca-135">È possibile creare una pipeline con un'attività di copia per spostare i dati da un archivio dati DB2 usando diversi strumenti e API:</span><span class="sxs-lookup"><span data-stu-id="54fca-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="54fca-136">Il modo più semplice per creare una pipeline è usare la Copia guidata di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54fca-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="54fca-137">Per una rapida procedura dettagliata di creazione di una pipeline mediante la copia guidata dei dati, vedere [Esercitazione: Creare una pipeline con l'attività di copia usando la Copia guidata di Data Factory](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="54fca-138">Per creare una pipeline è possibile anche usare strumenti come il portale di Azure, Visual Studio, Azure PowerShell, un modello di Azure Resource Manager, l'API .NET e l'API REST.</span><span class="sxs-lookup"><span data-stu-id="54fca-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="54fca-139">Per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia, vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="54fca-140">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="54fca-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="54fca-141">Creare i servizi collegati per collegare gli archivi dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="54fca-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="54fca-142">Creare i set di dati per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="54fca-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="54fca-143">Creare una pipeline con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="54fca-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="54fca-144">Quando si usa la Copia guidata, le definizioni JSON per i servizi collegati, i set di dati e le entità pipeline di data factory vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="54fca-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="54fca-145">Quando si usano gli strumenti o le API, ad eccezione dell'API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54fca-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="54fca-146">La sezione [Esempio JSON: Copiare dati da DB2 a BLOB di Azure](#json-example-copy-data-from-db2-to-azure-blob) mostra le definizioni JSON per le entità di Data Factory utilizzate per copiare dati da un archivio dati DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="54fca-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="54fca-147">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di Data Factory specifiche di un archivio dati DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="54fca-148">Proprietà del servizio collegato DB2</span><span class="sxs-lookup"><span data-stu-id="54fca-148">DB2 linked service properties</span></span>
<span data-ttu-id="54fca-149">La tabella seguente elenca le proprietà JSON che sono specifiche di un servizio collegato DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="54fca-150">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54fca-150">Property</span></span> | <span data-ttu-id="54fca-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54fca-151">Description</span></span> | <span data-ttu-id="54fca-152">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54fca-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fca-153">**type**</span><span class="sxs-lookup"><span data-stu-id="54fca-153">**type**</span></span> |<span data-ttu-id="54fca-154">Questa proprietà deve essere impostata su **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="54fca-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="54fca-155">Sì</span><span class="sxs-lookup"><span data-stu-id="54fca-155">Yes</span></span> |
| <span data-ttu-id="54fca-156">**server**</span><span class="sxs-lookup"><span data-stu-id="54fca-156">**server**</span></span> |<span data-ttu-id="54fca-157">Il nome del server DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-157">The name of the DB2 server.</span></span> |<span data-ttu-id="54fca-158">Sì</span><span class="sxs-lookup"><span data-stu-id="54fca-158">Yes</span></span> |
| <span data-ttu-id="54fca-159">**database**</span><span class="sxs-lookup"><span data-stu-id="54fca-159">**database**</span></span> |<span data-ttu-id="54fca-160">Il nome del database DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-160">The name of the DB2 database.</span></span> |<span data-ttu-id="54fca-161">Sì</span><span class="sxs-lookup"><span data-stu-id="54fca-161">Yes</span></span> |
| <span data-ttu-id="54fca-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="54fca-162">**schema**</span></span> |<span data-ttu-id="54fca-163">Il nome dello schema nel database DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="54fca-164">Questa proprietà fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54fca-164">This property is case-sensitive.</span></span> |<span data-ttu-id="54fca-165">No</span><span class="sxs-lookup"><span data-stu-id="54fca-165">No</span></span> |
| <span data-ttu-id="54fca-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="54fca-166">**authenticationType**</span></span> |<span data-ttu-id="54fca-167">Il tipo di autenticazione utilizzato per connettersi al database DB2.</span><span class="sxs-lookup"><span data-stu-id="54fca-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="54fca-168">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="54fca-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="54fca-169">Sì</span><span class="sxs-lookup"><span data-stu-id="54fca-169">Yes</span></span> |
| <span data-ttu-id="54fca-170">**username**</span><span class="sxs-lookup"><span data-stu-id="54fca-170">**username**</span></span> |<span data-ttu-id="54fca-171">Il nome dell'account utente, se si usa l'autenticazione di base o di Windows.</span><span class="sxs-lookup"><span data-stu-id="54fca-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="54fca-172">No</span><span class="sxs-lookup"><span data-stu-id="54fca-172">No</span></span> |
| <span data-ttu-id="54fca-173">**password**</span><span class="sxs-lookup"><span data-stu-id="54fca-173">**password**</span></span> |<span data-ttu-id="54fca-174">La password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="54fca-174">The password for the user account.</span></span> |<span data-ttu-id="54fca-175">No</span><span class="sxs-lookup"><span data-stu-id="54fca-175">No</span></span> |
| <span data-ttu-id="54fca-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="54fca-176">**gatewayName**</span></span> |<span data-ttu-id="54fca-177">Il nome del gateway che il servizio Data factory deve usare per connettersi al database DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="54fca-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="54fca-178">Sì</span><span class="sxs-lookup"><span data-stu-id="54fca-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="54fca-179">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="54fca-179">Dataset properties</span></span>
<span data-ttu-id="54fca-180">Per un elenco delle sezioni e delle proprietà disponibili per la definizione dei set di dati, vedere l'articolo [Set di dati in Azure Data Factory](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="54fca-181">Le sezioni come **struttura**, **disponibilità** e **policy** di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, archiviazione BLOB di Azure, archiviazione tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="54fca-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="54fca-182">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="54fca-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="54fca-183">La sezione **typeProperties** per il set di dati di tipo **RelationalTable**, che comprende il set di dati DB2, presenta la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="54fca-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="54fca-184">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54fca-184">Property</span></span> | <span data-ttu-id="54fca-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54fca-185">Description</span></span> | <span data-ttu-id="54fca-186">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54fca-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fca-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="54fca-187">**tableName**</span></span> |<span data-ttu-id="54fca-188">Il nome della tabella nell'istanza del database DB2 a cui il servizio collegato fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="54fca-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="54fca-189">Questa proprietà fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54fca-189">This property is case-sensitive.</span></span> |<span data-ttu-id="54fca-190">No (se è specificata la proprietà **query** di un'attività di copia di tipo **RelationalSource**)</span><span class="sxs-lookup"><span data-stu-id="54fca-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="54fca-191">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="54fca-191">Copy Activity properties</span></span>
<span data-ttu-id="54fca-192">Per un elenco delle sezioni e delle proprietà disponibili per la definizione delle attività di copia, vedere l'articolo relativo alla [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="54fca-193">Per tutti i tipi di attività sono disponibili le proprietà dell'attività di copia, come **name**, **description**, tabella **inputs**, tabella **outputs** e **policy**.</span><span class="sxs-lookup"><span data-stu-id="54fca-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="54fca-194">Le proprietà disponibili nella sezione **typeProperties** dell'attività per ciascun tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="54fca-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="54fca-195">Per l'attività di copia, le proprietà variano in base ai tipi di origini dati e sink.</span><span class="sxs-lookup"><span data-stu-id="54fca-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="54fca-196">Per le attività di copia con origine di tipo **RelationalSource** (che comprende DB2), sono disponibili le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="54fca-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="54fca-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="54fca-197">Property</span></span> | <span data-ttu-id="54fca-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="54fca-198">Description</span></span> | <span data-ttu-id="54fca-199">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="54fca-199">Allowed values</span></span> | <span data-ttu-id="54fca-200">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="54fca-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54fca-201">**query**</span><span class="sxs-lookup"><span data-stu-id="54fca-201">**query**</span></span> |<span data-ttu-id="54fca-202">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="54fca-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="54fca-203">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="54fca-203">SQL query string.</span></span> <span data-ttu-id="54fca-204">Ad esempio: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="54fca-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="54fca-205">No (se è specificata la proprietà **tableName** di un set di dati)</span><span class="sxs-lookup"><span data-stu-id="54fca-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="54fca-206">I nomi di schemi e tabelle fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54fca-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="54fca-207">Nell'istruzione della query racchiudere i nomi di proprietà fra virgolette doppie ("").</span><span class="sxs-lookup"><span data-stu-id="54fca-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="54fca-208">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="54fca-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="54fca-209">Esempio JSON: Copiare dati da DB2 a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="54fca-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="54fca-210">Questo esempio fornisce le definizioni JSON di esempio da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="54fca-211">L'esempio illustra come copiare dati da un database DB2 nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="54fca-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="54fca-212">Tuttavia, è possibile copiare i dati in [qualsiasi tipo di sink di archivio dati supportato](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54fca-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="54fca-213">L'esempio include le entità della data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="54fca-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="54fca-214">Un servizio collegato DB2 di tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="54fca-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="54fca-215">Un servizio collegato di archiviazione BLOB di Azure di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="54fca-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="54fca-216">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="54fca-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="54fca-217">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="54fca-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="54fca-218">Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa le proprietà [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="54fca-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="54fca-219">L'esempio copia i dati da un risultato della query in un database DB2 a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="54fca-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="54fca-220">Le proprietà JSON utilizzate in questi esempi sono descritte nelle sezioni riportate dopo le definizioni di entità.</span><span class="sxs-lookup"><span data-stu-id="54fca-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="54fca-221">Innanzitutto installare e configurare un gateway dati.</span><span class="sxs-lookup"><span data-stu-id="54fca-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="54fca-222">Le istruzioni si trovano nell'articolo [Spostare dati tra percorsi locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="54fca-223">**Servizio collegato DB2**</span><span class="sxs-lookup"><span data-stu-id="54fca-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

<span data-ttu-id="54fca-224">**Servizio collegato di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="54fca-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="54fca-225">**Set di dati di input DB2**</span><span class="sxs-lookup"><span data-stu-id="54fca-225">**DB2 input dataset**</span></span>

<span data-ttu-id="54fca-226">L'esempio presuppone che sia stata creata una tabella in DB2 denominata "MyTable" contenente una colonna denominata "timestamp" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="54fca-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="54fca-227">La proprietà **external** è impostata su "true".</span><span class="sxs-lookup"><span data-stu-id="54fca-227">The **external** property is set to "true."</span></span> <span data-ttu-id="54fca-228">Questa impostazione comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è generato da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="54fca-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="54fca-229">Si noti che il valore della proprietà **type** è impostato su **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="54fca-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="54fca-230">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="54fca-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="54fca-231">I dati vengono scritti in un nuovo BLOB ogni ora impostando la proprietà **frequency** su "Hour" e **interval** su 1.</span><span class="sxs-lookup"><span data-stu-id="54fca-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="54fca-232">La proprietà **folderPath** per il BLOB viene valutata dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="54fca-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="54fca-233">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="54fca-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="54fca-234">**Pipeline con l'attività di copia**</span><span class="sxs-lookup"><span data-stu-id="54fca-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="54fca-235">La pipeline contiene un'attività di copia configurata per usare set di dati di input e output specificati e programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="54fca-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="54fca-236">Nella definizione JSON per la pipeline il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="54fca-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="54fca-237">La query SQL specificata per la proprietà **query** seleziona i dati dalla tabella "Orders".</span><span class="sxs-lookup"><span data-stu-id="54fca-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="54fca-238">Mapping dei tipi per DB2</span><span class="sxs-lookup"><span data-stu-id="54fca-238">Type mapping for DB2</span></span>
<span data-ttu-id="54fca-239">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md), l'attività di copia esegue conversioni di tipo automatiche dai tipi di origine ai tipi di sink usando l'approccio in due passaggi seguente:</span><span class="sxs-lookup"><span data-stu-id="54fca-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="54fca-240">Conversione dal tipo di origine nativo al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="54fca-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="54fca-241">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="54fca-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="54fca-242">Quando l'attività di copia converte i dati da un tipo DB2 in un tipo .NET, vengono utilizzati i mapping seguenti:</span><span class="sxs-lookup"><span data-stu-id="54fca-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="54fca-243">Tipo di database DB2</span><span class="sxs-lookup"><span data-stu-id="54fca-243">DB2 database type</span></span> | <span data-ttu-id="54fca-244">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="54fca-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="54fca-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="54fca-245">SmallInt</span></span> |<span data-ttu-id="54fca-246">Int16</span><span class="sxs-lookup"><span data-stu-id="54fca-246">Int16</span></span> |
| <span data-ttu-id="54fca-247">Integer</span><span class="sxs-lookup"><span data-stu-id="54fca-247">Integer</span></span> |<span data-ttu-id="54fca-248">Int32</span><span class="sxs-lookup"><span data-stu-id="54fca-248">Int32</span></span> |
| <span data-ttu-id="54fca-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="54fca-249">BigInt</span></span> |<span data-ttu-id="54fca-250">Int64</span><span class="sxs-lookup"><span data-stu-id="54fca-250">Int64</span></span> |
| <span data-ttu-id="54fca-251">Real</span><span class="sxs-lookup"><span data-stu-id="54fca-251">Real</span></span> |<span data-ttu-id="54fca-252">Single</span><span class="sxs-lookup"><span data-stu-id="54fca-252">Single</span></span> |
| <span data-ttu-id="54fca-253">Double</span><span class="sxs-lookup"><span data-stu-id="54fca-253">Double</span></span> |<span data-ttu-id="54fca-254">Double</span><span class="sxs-lookup"><span data-stu-id="54fca-254">Double</span></span> |
| <span data-ttu-id="54fca-255">Float</span><span class="sxs-lookup"><span data-stu-id="54fca-255">Float</span></span> |<span data-ttu-id="54fca-256">Double</span><span class="sxs-lookup"><span data-stu-id="54fca-256">Double</span></span> |
| <span data-ttu-id="54fca-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-257">Decimal</span></span> |<span data-ttu-id="54fca-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-258">Decimal</span></span> |
| <span data-ttu-id="54fca-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="54fca-259">DecimalFloat</span></span> |<span data-ttu-id="54fca-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-260">Decimal</span></span> |
| <span data-ttu-id="54fca-261">Numeric</span><span class="sxs-lookup"><span data-stu-id="54fca-261">Numeric</span></span> |<span data-ttu-id="54fca-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-262">Decimal</span></span> |
| <span data-ttu-id="54fca-263">Date</span><span class="sxs-lookup"><span data-stu-id="54fca-263">Date</span></span> |<span data-ttu-id="54fca-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="54fca-264">DateTime</span></span> |
| <span data-ttu-id="54fca-265">Time</span><span class="sxs-lookup"><span data-stu-id="54fca-265">Time</span></span> |<span data-ttu-id="54fca-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="54fca-266">TimeSpan</span></span> |
| <span data-ttu-id="54fca-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="54fca-267">Timestamp</span></span> |<span data-ttu-id="54fca-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="54fca-268">DateTime</span></span> |
| <span data-ttu-id="54fca-269">xml</span><span class="sxs-lookup"><span data-stu-id="54fca-269">Xml</span></span> |<span data-ttu-id="54fca-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="54fca-270">Byte[]</span></span> |
| <span data-ttu-id="54fca-271">Char</span><span class="sxs-lookup"><span data-stu-id="54fca-271">Char</span></span> |<span data-ttu-id="54fca-272">String</span><span class="sxs-lookup"><span data-stu-id="54fca-272">String</span></span> |
| <span data-ttu-id="54fca-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="54fca-273">VarChar</span></span> |<span data-ttu-id="54fca-274">String</span><span class="sxs-lookup"><span data-stu-id="54fca-274">String</span></span> |
| <span data-ttu-id="54fca-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="54fca-275">LongVarChar</span></span> |<span data-ttu-id="54fca-276">String</span><span class="sxs-lookup"><span data-stu-id="54fca-276">String</span></span> |
| <span data-ttu-id="54fca-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="54fca-277">DB2DynArray</span></span> |<span data-ttu-id="54fca-278">String</span><span class="sxs-lookup"><span data-stu-id="54fca-278">String</span></span> |
| <span data-ttu-id="54fca-279">Binary</span><span class="sxs-lookup"><span data-stu-id="54fca-279">Binary</span></span> |<span data-ttu-id="54fca-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="54fca-280">Byte[]</span></span> |
| <span data-ttu-id="54fca-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="54fca-281">VarBinary</span></span> |<span data-ttu-id="54fca-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="54fca-282">Byte[]</span></span> |
| <span data-ttu-id="54fca-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="54fca-283">LongVarBinary</span></span> |<span data-ttu-id="54fca-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="54fca-284">Byte[]</span></span> |
| <span data-ttu-id="54fca-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="54fca-285">Graphic</span></span> |<span data-ttu-id="54fca-286">String</span><span class="sxs-lookup"><span data-stu-id="54fca-286">String</span></span> |
| <span data-ttu-id="54fca-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="54fca-287">VarGraphic</span></span> |<span data-ttu-id="54fca-288">String</span><span class="sxs-lookup"><span data-stu-id="54fca-288">String</span></span> |
| <span data-ttu-id="54fca-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="54fca-289">LongVarGraphic</span></span> |<span data-ttu-id="54fca-290">String</span><span class="sxs-lookup"><span data-stu-id="54fca-290">String</span></span> |
| <span data-ttu-id="54fca-291">Clob</span><span class="sxs-lookup"><span data-stu-id="54fca-291">Clob</span></span> |<span data-ttu-id="54fca-292">String</span><span class="sxs-lookup"><span data-stu-id="54fca-292">String</span></span> |
| <span data-ttu-id="54fca-293">BLOB</span><span class="sxs-lookup"><span data-stu-id="54fca-293">Blob</span></span> |<span data-ttu-id="54fca-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="54fca-294">Byte[]</span></span> |
| <span data-ttu-id="54fca-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="54fca-295">DbClob</span></span> |<span data-ttu-id="54fca-296">String</span><span class="sxs-lookup"><span data-stu-id="54fca-296">String</span></span> |
| <span data-ttu-id="54fca-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="54fca-297">SmallInt</span></span> |<span data-ttu-id="54fca-298">Int16</span><span class="sxs-lookup"><span data-stu-id="54fca-298">Int16</span></span> |
| <span data-ttu-id="54fca-299">Integer</span><span class="sxs-lookup"><span data-stu-id="54fca-299">Integer</span></span> |<span data-ttu-id="54fca-300">Int32</span><span class="sxs-lookup"><span data-stu-id="54fca-300">Int32</span></span> |
| <span data-ttu-id="54fca-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="54fca-301">BigInt</span></span> |<span data-ttu-id="54fca-302">Int64</span><span class="sxs-lookup"><span data-stu-id="54fca-302">Int64</span></span> |
| <span data-ttu-id="54fca-303">Real</span><span class="sxs-lookup"><span data-stu-id="54fca-303">Real</span></span> |<span data-ttu-id="54fca-304">Single</span><span class="sxs-lookup"><span data-stu-id="54fca-304">Single</span></span> |
| <span data-ttu-id="54fca-305">Double</span><span class="sxs-lookup"><span data-stu-id="54fca-305">Double</span></span> |<span data-ttu-id="54fca-306">Double</span><span class="sxs-lookup"><span data-stu-id="54fca-306">Double</span></span> |
| <span data-ttu-id="54fca-307">Float</span><span class="sxs-lookup"><span data-stu-id="54fca-307">Float</span></span> |<span data-ttu-id="54fca-308">Double</span><span class="sxs-lookup"><span data-stu-id="54fca-308">Double</span></span> |
| <span data-ttu-id="54fca-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-309">Decimal</span></span> |<span data-ttu-id="54fca-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-310">Decimal</span></span> |
| <span data-ttu-id="54fca-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="54fca-311">DecimalFloat</span></span> |<span data-ttu-id="54fca-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-312">Decimal</span></span> |
| <span data-ttu-id="54fca-313">Numeric</span><span class="sxs-lookup"><span data-stu-id="54fca-313">Numeric</span></span> |<span data-ttu-id="54fca-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="54fca-314">Decimal</span></span> |
| <span data-ttu-id="54fca-315">Date</span><span class="sxs-lookup"><span data-stu-id="54fca-315">Date</span></span> |<span data-ttu-id="54fca-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="54fca-316">DateTime</span></span> |
| <span data-ttu-id="54fca-317">Time</span><span class="sxs-lookup"><span data-stu-id="54fca-317">Time</span></span> |<span data-ttu-id="54fca-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="54fca-318">TimeSpan</span></span> |
| <span data-ttu-id="54fca-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="54fca-319">Timestamp</span></span> |<span data-ttu-id="54fca-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="54fca-320">DateTime</span></span> |
| <span data-ttu-id="54fca-321">xml</span><span class="sxs-lookup"><span data-stu-id="54fca-321">Xml</span></span> |<span data-ttu-id="54fca-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="54fca-322">Byte[]</span></span> |
| <span data-ttu-id="54fca-323">Char</span><span class="sxs-lookup"><span data-stu-id="54fca-323">Char</span></span> |<span data-ttu-id="54fca-324">String</span><span class="sxs-lookup"><span data-stu-id="54fca-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="54fca-325">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="54fca-325">Map source to sink columns</span></span>
<span data-ttu-id="54fca-326">Per informazioni su come eseguire il mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="54fca-327">Letture ripetibili da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="54fca-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="54fca-328">Quando si copiano dati da un archivio dati relazionale è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="54fca-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="54fca-329">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="54fca-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="54fca-330">È anche possibile configurare la proprietà **policy** di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="54fca-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="54fca-331">Assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione e dal modo in cui la sezione viene rieseguita.</span><span class="sxs-lookup"><span data-stu-id="54fca-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="54fca-332">Per altre informazioni, vedere [Letture ripetibili da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="54fca-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="54fca-333">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="54fca-333">Performance and tuning</span></span>
<span data-ttu-id="54fca-334">Per informazioni sui fattori chiave che influiscono sulle prestazioni dell'attività di copia e sui modi per ottimizzarle, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="54fca-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>