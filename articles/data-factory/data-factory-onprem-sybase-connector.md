---
title: aaaMove dati da Sybase utilizzando Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati dal Database di Sybase utilizzando Data Factory di Azure.
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
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="75c5e-103">Spostare i dati da Sybase utilizzando Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="75c5e-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="75c5e-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="75c5e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="75c5e-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="75c5e-106">È possibile copiare dati da un archivio di dati di on-premise Sybase dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="75c5e-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="75c5e-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="75c5e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="75c5e-108">Data factory di attualmente supporta solo lo spostamento di dati da un Sybase archiviano tooother archivi di dati, ma non per lo spostamento dei dati da altro archivio dati di Sybase tooa di archivi di dati.</span><span class="sxs-lookup"><span data-stu-id="75c5e-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="75c5e-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="75c5e-109">Prerequisites</span></span>
<span data-ttu-id="75c5e-110">Servizio Data Factory supporta origini di Sybase locale tooon connessione hello Gateway di gestione dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="75c5e-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="75c5e-111">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="75c5e-112">Anche se il database di Sybase hello è ospitato in una macchina virtuale IaaS di Azure, è necessario gateway.</span><span class="sxs-lookup"><span data-stu-id="75c5e-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="75c5e-113">È possibile installare il gateway di hello in hello stessa VM IaaS come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="75c5e-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="75c5e-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="75c5e-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="75c5e-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="75c5e-115">Supported versions and installation</span></span>
<span data-ttu-id="75c5e-116">Per Gateway di gestione dati tooconnect toohello Sybase Database, è necessario hello tooinstall [provider di dati per Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 o sopra in hello stesso sistema come hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="75c5e-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="75c5e-117">Sono supportate le versioni di Sybase a partire dalla 16.</span><span class="sxs-lookup"><span data-stu-id="75c5e-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="75c5e-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="75c5e-118">Getting started</span></span>
<span data-ttu-id="75c5e-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="75c5e-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="75c5e-120">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="75c5e-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="75c5e-121">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="75c5e-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="75c5e-122">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="75c5e-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="75c5e-123">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="75c5e-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="75c5e-124">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="75c5e-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="75c5e-125">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="75c5e-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="75c5e-126">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="75c5e-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="75c5e-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="75c5e-128">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="75c5e-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="75c5e-129">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="75c5e-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="75c5e-130">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati di Sybase locale, vedere [esempio JSON: copiare i dati da Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="75c5e-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="75c5e-131">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa Sybase:</span><span class="sxs-lookup"><span data-stu-id="75c5e-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="75c5e-132">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="75c5e-132">Linked service properties</span></span>
<span data-ttu-id="75c5e-133">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooSybase collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="75c5e-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="75c5e-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="75c5e-134">Property</span></span> | <span data-ttu-id="75c5e-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="75c5e-135">Description</span></span> | <span data-ttu-id="75c5e-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="75c5e-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="75c5e-137">type</span><span class="sxs-lookup"><span data-stu-id="75c5e-137">type</span></span> |<span data-ttu-id="75c5e-138">proprietà di tipo Hello deve essere impostata su: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="75c5e-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="75c5e-139">Sì</span><span class="sxs-lookup"><span data-stu-id="75c5e-139">Yes</span></span> |
| <span data-ttu-id="75c5e-140">server</span><span class="sxs-lookup"><span data-stu-id="75c5e-140">server</span></span> |<span data-ttu-id="75c5e-141">Nome del server di Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="75c5e-142">Sì</span><span class="sxs-lookup"><span data-stu-id="75c5e-142">Yes</span></span> |
| <span data-ttu-id="75c5e-143">database</span><span class="sxs-lookup"><span data-stu-id="75c5e-143">database</span></span> |<span data-ttu-id="75c5e-144">Nome del database di Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="75c5e-145">Sì</span><span class="sxs-lookup"><span data-stu-id="75c5e-145">Yes</span></span> |
| <span data-ttu-id="75c5e-146">schema</span><span class="sxs-lookup"><span data-stu-id="75c5e-146">schema</span></span> |<span data-ttu-id="75c5e-147">Nome dello schema hello nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="75c5e-148">No</span><span class="sxs-lookup"><span data-stu-id="75c5e-148">No</span></span> |
| <span data-ttu-id="75c5e-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="75c5e-149">authenticationType</span></span> |<span data-ttu-id="75c5e-150">Tipo di autenticazione usato tooconnect toohello database di Sybase.</span><span class="sxs-lookup"><span data-stu-id="75c5e-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="75c5e-151">I valori possibili sono: anonima, di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="75c5e-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="75c5e-152">Sì</span><span class="sxs-lookup"><span data-stu-id="75c5e-152">Yes</span></span> |
| <span data-ttu-id="75c5e-153">username</span><span class="sxs-lookup"><span data-stu-id="75c5e-153">username</span></span> |<span data-ttu-id="75c5e-154">Specificare il nome utente se si usa l'autenticazione di base o Windows.</span><span class="sxs-lookup"><span data-stu-id="75c5e-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="75c5e-155">No</span><span class="sxs-lookup"><span data-stu-id="75c5e-155">No</span></span> |
| <span data-ttu-id="75c5e-156">password</span><span class="sxs-lookup"><span data-stu-id="75c5e-156">password</span></span> |<span data-ttu-id="75c5e-157">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="75c5e-158">No</span><span class="sxs-lookup"><span data-stu-id="75c5e-158">No</span></span> |
| <span data-ttu-id="75c5e-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="75c5e-159">gatewayName</span></span> |<span data-ttu-id="75c5e-160">Nome del gateway hello hello servizio Data Factory deve usare database di Sybase tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="75c5e-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="75c5e-161">Sì</span><span class="sxs-lookup"><span data-stu-id="75c5e-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="75c5e-162">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="75c5e-162">Dataset properties</span></span>
<span data-ttu-id="75c5e-163">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="75c5e-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="75c5e-164">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="75c5e-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="75c5e-165">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="75c5e-166">Hello **typeProperties** sezione per set di dati di tipo **RelationalTable** (che include set di dati Sybase) ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="75c5e-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="75c5e-167">Proprietà</span><span class="sxs-lookup"><span data-stu-id="75c5e-167">Property</span></span> | <span data-ttu-id="75c5e-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="75c5e-168">Description</span></span> | <span data-ttu-id="75c5e-169">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="75c5e-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="75c5e-170">tableName</span><span class="sxs-lookup"><span data-stu-id="75c5e-170">tableName</span></span> |<span data-ttu-id="75c5e-171">Nome della tabella hello in hello istanza del Database di Sybase riferito al servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="75c5e-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="75c5e-172">No (se la **query** di **RelationalSource** è specificata)</span><span class="sxs-lookup"><span data-stu-id="75c5e-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="75c5e-173">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="75c5e-173">Copy activity properties</span></span>
<span data-ttu-id="75c5e-174">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="75c5e-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="75c5e-175">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="75c5e-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="75c5e-176">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="75c5e-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="75c5e-177">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="75c5e-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="75c5e-178">Quando origine hello è di tipo **RelationalSource** (che include Sybase), hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="75c5e-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="75c5e-179">Proprietà</span><span class="sxs-lookup"><span data-stu-id="75c5e-179">Property</span></span> | <span data-ttu-id="75c5e-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="75c5e-180">Description</span></span> | <span data-ttu-id="75c5e-181">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="75c5e-181">Allowed values</span></span> | <span data-ttu-id="75c5e-182">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="75c5e-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75c5e-183">query</span><span class="sxs-lookup"><span data-stu-id="75c5e-183">query</span></span> |<span data-ttu-id="75c5e-184">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="75c5e-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="75c5e-185">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="75c5e-185">SQL query string.</span></span> <span data-ttu-id="75c5e-186">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="75c5e-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="75c5e-187">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="75c5e-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="75c5e-188">Esempio JSON: copiare i dati da Sybase tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="75c5e-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="75c5e-189">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="75c5e-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="75c5e-190">Visualizzano toocopy dati da Sybase database tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="75c5e-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="75c5e-191">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="75c5e-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="75c5e-192">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="75c5e-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="75c5e-193">Un servizio collegato di tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="75c5e-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="75c5e-194">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="75c5e-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="75c5e-195">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="75c5e-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="75c5e-196">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="75c5e-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="75c5e-197">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="75c5e-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="75c5e-198">esempio Hello copia dati da un risultato di query nell'oggetto blob tooa database Sybase ogni ora.</span><span class="sxs-lookup"><span data-stu-id="75c5e-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="75c5e-199">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="75c5e-200">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="75c5e-201">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="75c5e-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="75c5e-202">**Servizio collegato Sybase:**</span><span class="sxs-lookup"><span data-stu-id="75c5e-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="75c5e-203">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="75c5e-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="75c5e-204">**Set di dati di input Sybase:**</span><span class="sxs-lookup"><span data-stu-id="75c5e-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="75c5e-205">esempio Hello presuppone di aver creato una tabella "MyTable" in Sybase e contiene una colonna denominata "timestamp" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="75c5e-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="75c5e-206">L'impostazione "external": true informa il servizio di Data Factory hello che questo set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="75c5e-207">Si noti che hello **tipo** di hello servizio collegato è impostato su: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="75c5e-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="75c5e-208">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="75c5e-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="75c5e-209">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="75c5e-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="75c5e-210">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="75c5e-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="75c5e-211">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="75c5e-212">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="75c5e-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="75c5e-213">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e si svolge ogni ora toorun pianificato.</span><span class="sxs-lookup"><span data-stu-id="75c5e-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="75c5e-214">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="75c5e-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="75c5e-215">query SQL Hello specificata per hello **query** proprietà vengono selezionati dati hello hello DBA. Tabella Orders nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="75c5e-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="75c5e-216">Mapping dei tipi per Sybase</span><span class="sxs-lookup"><span data-stu-id="75c5e-216">Type mapping for Sybase</span></span>
<span data-ttu-id="75c5e-217">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo hello attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="75c5e-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="75c5e-218">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="75c5e-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="75c5e-219">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="75c5e-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="75c5e-220">Sybase supporta i tipi T-SQL e T-SQL.</span><span class="sxs-lookup"><span data-stu-id="75c5e-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="75c5e-221">Per una tabella di mapping dal tipo di too.NET tipi sql, vedere [connettore di SQL Azure](data-factory-azure-sql-connector.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="75c5e-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="75c5e-222">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="75c5e-222">Map source toosink columns</span></span>
<span data-ttu-id="75c5e-223">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="75c5e-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="75c5e-224">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="75c5e-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="75c5e-225">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="75c5e-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="75c5e-226">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="75c5e-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="75c5e-227">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="75c5e-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="75c5e-228">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="75c5e-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="75c5e-229">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="75c5e-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="75c5e-230">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="75c5e-230">Performance and Tuning</span></span>
<span data-ttu-id="75c5e-231">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="75c5e-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
