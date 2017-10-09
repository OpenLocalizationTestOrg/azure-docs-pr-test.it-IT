---
title: dati aaaMove da PostgreSQL utilizzando Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati dal PostgreSQL Database usando Azure Data Factory.
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
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="cb4f8-103">Spostare i dati da PostgreSQL mediante Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="cb4f8-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="cb4f8-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="cb4f8-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="cb4f8-106">È possibile copiare dati da un archivio di dati di on-premise PostgreSQL dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="cb4f8-107">Per un elenco di archivi dati come sink è supportato dall'attività di copia hello, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="cb4f8-108">Data factory di attualmente supporta lo spostamento di dati da un PostgreSQL database tooother archivi dati, ma non per lo spostamento dei dati da altri dati vengono archiviati database PostgreSQL tooan.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cb4f8-109">prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cb4f8-109">prerequisites</span></span>

<span data-ttu-id="cb4f8-110">Servizio Data Factory supporta la connessione delle origini PostgreSQL locale tooon hello Gateway di gestione dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="cb4f8-111">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="cb4f8-112">Anche se database PostgreSQL hello è ospitato in una macchina virtuale IaaS di Azure, è necessario gateway.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="cb4f8-113">È possibile installare gateway in hello stessa VM IaaS come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="cb4f8-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="cb4f8-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="cb4f8-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="cb4f8-115">Supported versions and installation</span></span>
<span data-ttu-id="cb4f8-116">Per Gateway di gestione dati tooconnect toohello PostgreSQL Database, installare hello [Ngpsql i provider di dati per PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 o sopra in hello stesso sistema come hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="cb4f8-117">Sono supportate le versioni di PostgreSQL a partire dalla 7.4.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cb4f8-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="cb4f8-118">Getting started</span></span>
<span data-ttu-id="cb4f8-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati PostgreSQL usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="cb4f8-120">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cb4f8-121">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="cb4f8-122">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="cb4f8-123">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cb4f8-123">Azure portal</span></span>
    - <span data-ttu-id="cb4f8-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb4f8-124">Visual Studio</span></span>
    - <span data-ttu-id="cb4f8-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb4f8-125">Azure PowerShell</span></span>
    - <span data-ttu-id="cb4f8-126">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cb4f8-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="cb4f8-127">API .NET</span><span class="sxs-lookup"><span data-stu-id="cb4f8-127">.NET API</span></span>
    - <span data-ttu-id="cb4f8-128">API REST</span><span class="sxs-lookup"><span data-stu-id="cb4f8-128">REST API</span></span>

     <span data-ttu-id="cb4f8-129">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cb4f8-130">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="cb4f8-131">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="cb4f8-132">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="cb4f8-133">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="cb4f8-134">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cb4f8-135">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="cb4f8-136">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio di dati PostgreSQL locale, vedere [esempio JSON: copiare i dati da tooAzure PostgreSQL Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="cb4f8-137">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cb4f8-138">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="cb4f8-138">Linked service properties</span></span>
<span data-ttu-id="cb4f8-139">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooPostgreSQL collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="cb4f8-140">Proprietà</span><span class="sxs-lookup"><span data-stu-id="cb4f8-140">Property</span></span> | <span data-ttu-id="cb4f8-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cb4f8-141">Description</span></span> | <span data-ttu-id="cb4f8-142">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb4f8-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb4f8-143">type</span><span class="sxs-lookup"><span data-stu-id="cb4f8-143">type</span></span> |<span data-ttu-id="cb4f8-144">proprietà di tipo Hello deve essere impostata su: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="cb4f8-145">Sì</span><span class="sxs-lookup"><span data-stu-id="cb4f8-145">Yes</span></span> |
| <span data-ttu-id="cb4f8-146">server</span><span class="sxs-lookup"><span data-stu-id="cb4f8-146">server</span></span> |<span data-ttu-id="cb4f8-147">Nome del server PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="cb4f8-148">Sì</span><span class="sxs-lookup"><span data-stu-id="cb4f8-148">Yes</span></span> |
| <span data-ttu-id="cb4f8-149">database</span><span class="sxs-lookup"><span data-stu-id="cb4f8-149">database</span></span> |<span data-ttu-id="cb4f8-150">Nome del database PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="cb4f8-151">Sì</span><span class="sxs-lookup"><span data-stu-id="cb4f8-151">Yes</span></span> |
| <span data-ttu-id="cb4f8-152">schema</span><span class="sxs-lookup"><span data-stu-id="cb4f8-152">schema</span></span> |<span data-ttu-id="cb4f8-153">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="cb4f8-154">nome dello schema Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="cb4f8-155">No</span><span class="sxs-lookup"><span data-stu-id="cb4f8-155">No</span></span> |
| <span data-ttu-id="cb4f8-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cb4f8-156">authenticationType</span></span> |<span data-ttu-id="cb4f8-157">Tipo di autenticazione usato tooconnect toohello PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="cb4f8-158">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="cb4f8-159">Sì</span><span class="sxs-lookup"><span data-stu-id="cb4f8-159">Yes</span></span> |
| <span data-ttu-id="cb4f8-160">username</span><span class="sxs-lookup"><span data-stu-id="cb4f8-160">username</span></span> |<span data-ttu-id="cb4f8-161">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="cb4f8-162">No</span><span class="sxs-lookup"><span data-stu-id="cb4f8-162">No</span></span> |
| <span data-ttu-id="cb4f8-163">password</span><span class="sxs-lookup"><span data-stu-id="cb4f8-163">password</span></span> |<span data-ttu-id="cb4f8-164">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="cb4f8-165">No</span><span class="sxs-lookup"><span data-stu-id="cb4f8-165">No</span></span> |
| <span data-ttu-id="cb4f8-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cb4f8-166">gatewayName</span></span> |<span data-ttu-id="cb4f8-167">Nome del gateway hello hello servizio Data Factory deve utilizzare database PostgreSQL locale di tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="cb4f8-168">Sì</span><span class="sxs-lookup"><span data-stu-id="cb4f8-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="cb4f8-169">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="cb4f8-169">Dataset properties</span></span>
<span data-ttu-id="cb4f8-170">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cb4f8-171">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="cb4f8-172">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="cb4f8-173">sezione Hello typeProperties per set di dati di tipo **RelationalTable** (che include set di dati PostgreSQL) ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="cb4f8-174">Proprietà</span><span class="sxs-lookup"><span data-stu-id="cb4f8-174">Property</span></span> | <span data-ttu-id="cb4f8-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cb4f8-175">Description</span></span> | <span data-ttu-id="cb4f8-176">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb4f8-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb4f8-177">tableName</span><span class="sxs-lookup"><span data-stu-id="cb4f8-177">tableName</span></span> |<span data-ttu-id="cb4f8-178">Nome della tabella hello in hello istanza PostgreSQL Database riferito al servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="cb4f8-179">tableName Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="cb4f8-180">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="cb4f8-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="cb4f8-181">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="cb4f8-181">Copy activity properties</span></span>
<span data-ttu-id="cb4f8-182">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cb4f8-183">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="cb4f8-184">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="cb4f8-185">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="cb4f8-186">Quando l'origine è di tipo **RelationalSource** (che include PostgreSQL), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="cb4f8-187">Proprietà</span><span class="sxs-lookup"><span data-stu-id="cb4f8-187">Property</span></span> | <span data-ttu-id="cb4f8-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cb4f8-188">Description</span></span> | <span data-ttu-id="cb4f8-189">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="cb4f8-189">Allowed values</span></span> | <span data-ttu-id="cb4f8-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb4f8-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb4f8-191">query</span><span class="sxs-lookup"><span data-stu-id="cb4f8-191">query</span></span> |<span data-ttu-id="cb4f8-192">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="cb4f8-193">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-193">SQL query string.</span></span> <span data-ttu-id="cb4f8-194">Ad esempio: "query": "select * from \"Schema\".\"Tabella\"".</span><span class="sxs-lookup"><span data-stu-id="cb4f8-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="cb4f8-195">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="cb4f8-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="cb4f8-196">I nomi di schemi e tabelle fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="cb4f8-197">Racchiuderle tra istruzioni `""` (virgolette doppie) nella query hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="cb4f8-198">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="cb4f8-199">Esempio JSON: copiare i dati da tooAzure PostgreSQL Blob</span><span class="sxs-lookup"><span data-stu-id="cb4f8-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="cb4f8-200">In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cb4f8-201">Visualizzano dati toocopy PostgreSQL database tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="cb4f8-202">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="cb4f8-203">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="cb4f8-204">Non include istruzioni dettagliate per la creazione di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="cb4f8-205">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="cb4f8-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="cb4f8-206">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="cb4f8-207">Un servizio collegato di tipo [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="cb4f8-208">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cb4f8-209">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cb4f8-210">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cb4f8-211">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cb4f8-212">esempio Hello copia dati da un risultato di query nell'oggetto blob tooa database PostgreSQL ogni ora.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="cb4f8-213">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cb4f8-214">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="cb4f8-215">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="cb4f8-216">**Servizio collegato PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-216">**PostgreSQL linked service:**</span></span>

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
<span data-ttu-id="cb4f8-217">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-217">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="cb4f8-218">**Set di dati di input PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="cb4f8-219">esempio Hello presuppone aver creato una tabella "MyTable" nella PostgreSQL e contiene una colonna denominata "timestamp" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="cb4f8-220">Impostazione `"external": true` informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="cb4f8-221">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cb4f8-222">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cb4f8-223">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cb4f8-224">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="cb4f8-225">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="cb4f8-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="cb4f8-226">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e si svolge ogni ora toorun pianificato.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="cb4f8-227">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="cb4f8-228">query SQL Hello specificata per hello **query** proprietà Seleziona dati hello hello public.usstates tabella nel database PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

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
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="cb4f8-229">Mapping dei tipi per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cb4f8-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="cb4f8-230">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="cb4f8-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="cb4f8-231">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="cb4f8-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="cb4f8-232">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="cb4f8-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="cb4f8-233">Quando si spostano dati tooPostgreSQL, hello mapping seguenti vengono utilizzati da PostgreSQL too.NET del tipo.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="cb4f8-234">Tipo di database PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cb4f8-234">PostgreSQL Database type</span></span> | <span data-ttu-id="cb4f8-235">Alias PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="cb4f8-235">PostgresSQL aliases</span></span> | <span data-ttu-id="cb4f8-236">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cb4f8-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb4f8-237">abstime</span><span class="sxs-lookup"><span data-stu-id="cb4f8-237">abstime</span></span> | |<span data-ttu-id="cb4f8-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="cb4f8-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="cb4f8-239">bigint</span><span class="sxs-lookup"><span data-stu-id="cb4f8-239">bigint</span></span> |<span data-ttu-id="cb4f8-240">int8</span><span class="sxs-lookup"><span data-stu-id="cb4f8-240">int8</span></span> |<span data-ttu-id="cb4f8-241">Int64</span><span class="sxs-lookup"><span data-stu-id="cb4f8-241">Int64</span></span> |
| <span data-ttu-id="cb4f8-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="cb4f8-242">bigserial</span></span> |<span data-ttu-id="cb4f8-243">serial8</span><span class="sxs-lookup"><span data-stu-id="cb4f8-243">serial8</span></span> |<span data-ttu-id="cb4f8-244">Int64</span><span class="sxs-lookup"><span data-stu-id="cb4f8-244">Int64</span></span> |
| <span data-ttu-id="cb4f8-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-245">bit [ (n) ]</span></span> | |<span data-ttu-id="cb4f8-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="cb4f8-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="cb4f8-248">varbit</span><span class="sxs-lookup"><span data-stu-id="cb4f8-248">varbit</span></span> |<span data-ttu-id="cb4f8-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-249">Byte[], String</span></span> |
| <span data-ttu-id="cb4f8-250">boolean</span><span class="sxs-lookup"><span data-stu-id="cb4f8-250">boolean</span></span> |<span data-ttu-id="cb4f8-251">bool</span><span class="sxs-lookup"><span data-stu-id="cb4f8-251">bool</span></span> |<span data-ttu-id="cb4f8-252">boolean</span><span class="sxs-lookup"><span data-stu-id="cb4f8-252">Boolean</span></span> |
| <span data-ttu-id="cb4f8-253">box</span><span class="sxs-lookup"><span data-stu-id="cb4f8-253">box</span></span> | |<span data-ttu-id="cb4f8-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-255">bytea</span><span class="sxs-lookup"><span data-stu-id="cb4f8-255">bytea</span></span> | |<span data-ttu-id="cb4f8-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-257">character [ (n) ]</span></span> |<span data-ttu-id="cb4f8-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-258">char [ (n) ]</span></span> |<span data-ttu-id="cb4f8-259">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-259">String</span></span> |
| <span data-ttu-id="cb4f8-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-260">character varying [ (n) ]</span></span> |<span data-ttu-id="cb4f8-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-261">varchar [ (n) ]</span></span> |<span data-ttu-id="cb4f8-262">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-262">String</span></span> |
| <span data-ttu-id="cb4f8-263">cid</span><span class="sxs-lookup"><span data-stu-id="cb4f8-263">cid</span></span> | |<span data-ttu-id="cb4f8-264">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-264">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-265">cidr</span><span class="sxs-lookup"><span data-stu-id="cb4f8-265">cidr</span></span> | |<span data-ttu-id="cb4f8-266">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-266">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-267">circle</span><span class="sxs-lookup"><span data-stu-id="cb4f8-267">circle</span></span> | |<span data-ttu-id="cb4f8-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-269">date</span><span class="sxs-lookup"><span data-stu-id="cb4f8-269">date</span></span> | |<span data-ttu-id="cb4f8-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="cb4f8-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-271">daterange</span><span class="sxs-lookup"><span data-stu-id="cb4f8-271">daterange</span></span> | |<span data-ttu-id="cb4f8-272">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-272">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-273">double precision</span><span class="sxs-lookup"><span data-stu-id="cb4f8-273">double precision</span></span> |<span data-ttu-id="cb4f8-274">float8</span><span class="sxs-lookup"><span data-stu-id="cb4f8-274">float8</span></span> |<span data-ttu-id="cb4f8-275">Double</span><span class="sxs-lookup"><span data-stu-id="cb4f8-275">Double</span></span> |
| <span data-ttu-id="cb4f8-276">inet</span><span class="sxs-lookup"><span data-stu-id="cb4f8-276">inet</span></span> | |<span data-ttu-id="cb4f8-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-278">intarry</span><span class="sxs-lookup"><span data-stu-id="cb4f8-278">intarry</span></span> | |<span data-ttu-id="cb4f8-279">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-279">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-280">int4range</span><span class="sxs-lookup"><span data-stu-id="cb4f8-280">int4range</span></span> | |<span data-ttu-id="cb4f8-281">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-281">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-282">int8range</span><span class="sxs-lookup"><span data-stu-id="cb4f8-282">int8range</span></span> | |<span data-ttu-id="cb4f8-283">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-283">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-284">integer</span><span class="sxs-lookup"><span data-stu-id="cb4f8-284">integer</span></span> |<span data-ttu-id="cb4f8-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="cb4f8-285">int, int4</span></span> |<span data-ttu-id="cb4f8-286">Int32</span><span class="sxs-lookup"><span data-stu-id="cb4f8-286">Int32</span></span> |
| <span data-ttu-id="cb4f8-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="cb4f8-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="cb4f8-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-289">json</span><span class="sxs-lookup"><span data-stu-id="cb4f8-289">json</span></span> | |<span data-ttu-id="cb4f8-290">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-290">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="cb4f8-291">jsonb</span></span> | |<span data-ttu-id="cb4f8-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-293">line</span><span class="sxs-lookup"><span data-stu-id="cb4f8-293">line</span></span> | |<span data-ttu-id="cb4f8-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-295">lseg</span><span class="sxs-lookup"><span data-stu-id="cb4f8-295">lseg</span></span> | |<span data-ttu-id="cb4f8-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="cb4f8-297">macaddr</span></span> | |<span data-ttu-id="cb4f8-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-299">money</span><span class="sxs-lookup"><span data-stu-id="cb4f8-299">money</span></span> | |<span data-ttu-id="cb4f8-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="cb4f8-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="cb4f8-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="cb4f8-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="cb4f8-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="cb4f8-303">Decimal</span></span> |
| <span data-ttu-id="cb4f8-304">numrange</span><span class="sxs-lookup"><span data-stu-id="cb4f8-304">numrange</span></span> | |<span data-ttu-id="cb4f8-305">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-305">String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-306">oid</span><span class="sxs-lookup"><span data-stu-id="cb4f8-306">oid</span></span> | |<span data-ttu-id="cb4f8-307">Int32</span><span class="sxs-lookup"><span data-stu-id="cb4f8-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-308">path</span><span class="sxs-lookup"><span data-stu-id="cb4f8-308">path</span></span> | |<span data-ttu-id="cb4f8-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="cb4f8-310">pg_lsn</span></span> | |<span data-ttu-id="cb4f8-311">Int64</span><span class="sxs-lookup"><span data-stu-id="cb4f8-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-312">point</span><span class="sxs-lookup"><span data-stu-id="cb4f8-312">point</span></span> | |<span data-ttu-id="cb4f8-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-314">polygon</span><span class="sxs-lookup"><span data-stu-id="cb4f8-314">polygon</span></span> | |<span data-ttu-id="cb4f8-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="cb4f8-316">real</span><span class="sxs-lookup"><span data-stu-id="cb4f8-316">real</span></span> |<span data-ttu-id="cb4f8-317">float4</span><span class="sxs-lookup"><span data-stu-id="cb4f8-317">float4</span></span> |<span data-ttu-id="cb4f8-318">Single</span><span class="sxs-lookup"><span data-stu-id="cb4f8-318">Single</span></span> |
| <span data-ttu-id="cb4f8-319">smallint</span><span class="sxs-lookup"><span data-stu-id="cb4f8-319">smallint</span></span> |<span data-ttu-id="cb4f8-320">int2</span><span class="sxs-lookup"><span data-stu-id="cb4f8-320">int2</span></span> |<span data-ttu-id="cb4f8-321">Int16</span><span class="sxs-lookup"><span data-stu-id="cb4f8-321">Int16</span></span> |
| <span data-ttu-id="cb4f8-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="cb4f8-322">smallserial</span></span> |<span data-ttu-id="cb4f8-323">serial2</span><span class="sxs-lookup"><span data-stu-id="cb4f8-323">serial2</span></span> |<span data-ttu-id="cb4f8-324">Int16</span><span class="sxs-lookup"><span data-stu-id="cb4f8-324">Int16</span></span> |
| <span data-ttu-id="cb4f8-325">serial</span><span class="sxs-lookup"><span data-stu-id="cb4f8-325">serial</span></span> |<span data-ttu-id="cb4f8-326">serial4</span><span class="sxs-lookup"><span data-stu-id="cb4f8-326">serial4</span></span> |<span data-ttu-id="cb4f8-327">Int32</span><span class="sxs-lookup"><span data-stu-id="cb4f8-327">Int32</span></span> |
| <span data-ttu-id="cb4f8-328">text</span><span class="sxs-lookup"><span data-stu-id="cb4f8-328">text</span></span> | |<span data-ttu-id="cb4f8-329">String</span><span class="sxs-lookup"><span data-stu-id="cb4f8-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="cb4f8-330">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="cb4f8-330">Map source toosink columns</span></span>
<span data-ttu-id="cb4f8-331">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="cb4f8-332">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="cb4f8-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="cb4f8-333">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="cb4f8-334">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="cb4f8-335">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="cb4f8-336">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="cb4f8-337">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="cb4f8-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cb4f8-338">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="cb4f8-338">Performance and Tuning</span></span>
<span data-ttu-id="cb4f8-339">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="cb4f8-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
