---
title: aaaMove dati da SAP Business Warehouse utilizzando Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da SAP Business Warehouse usando Azure Data Factory.
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
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="d984e-103">Spostare dati da SAP Business Warehouse usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d984e-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="d984e-104">Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove da SAP Business Warehouse (BW) un locale.</span><span class="sxs-lookup"><span data-stu-id="d984e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="d984e-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d984e-106">È possibile copiare dati da un archivio di dati di on-premise SAP Business Warehouse dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="d984e-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="d984e-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="d984e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d984e-108">Data factory di supporta attualmente solo lo spostamento di dati da un tooother SAP Business Warehouse vengono archiviati, ma non per lo spostamento dei dati da altri dati archivia tooan SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d984e-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="d984e-109">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="d984e-109">Supported versions and installation</span></span>
<span data-ttu-id="d984e-110">Questo connettore supporta SAP Business Warehouse versione 7.x.</span><span class="sxs-lookup"><span data-stu-id="d984e-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="d984e-111">Supporta anche la copia di dati da Infocube e QueryCubes (incluse query BEx) tramite query MDX.</span><span class="sxs-lookup"><span data-stu-id="d984e-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="d984e-112">tooenable hello connettività toohello istanza SAP BW, installare hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="d984e-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="d984e-113">**Gateway di gestione dati**: servizio di Data Factory supporta la connessione dati locali tooon archivi (incluso SAP Business Warehouse) utilizzando un componente chiamato Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="d984e-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="d984e-114">toolearn sul Gateway di gestione dati e istruzioni dettagliate per la configurazione di gateway di hello, vedere [dati di spostamento tra i dati locali toocloud archiviano dati](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d984e-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="d984e-115">Gateway è necessario anche se hello SAP Business Warehouse è ospitato in una macchina virtuale IaaS di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="d984e-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="d984e-116">È possibile installare il gateway di hello in hello stessa macchina virtuale come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="d984e-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="d984e-117">**Libreria SAP NetWeaver** nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="d984e-118">È possibile ottenere libreria SAP Netweaver hello dall'amministratore di SAP o direttamente dal hello [area Download di Software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="d984e-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="d984e-119">Ricerca di hello **SAP nota #1025361** percorso di download di hello tooget per la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="d984e-120">Verificare che l'architettura di hello per la libreria di SAP NetWeaver hello (32 bit o 64 bit) corrisponda l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="d984e-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="d984e-121">Installare tutti i file inclusi in hello RFC SDK di SAP NetWeaver in base toohello nota SAP.</span><span class="sxs-lookup"><span data-stu-id="d984e-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="d984e-122">libreria di SAP NetWeaver Hello è anche inclusa nell'installazione di strumenti Client SAP hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="d984e-123">Inserire le DLL di hello estratte da hello SDK RFC NetWeaver nella cartella system32.</span><span class="sxs-lookup"><span data-stu-id="d984e-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d984e-124">introduttiva</span><span class="sxs-lookup"><span data-stu-id="d984e-124">Getting started</span></span>
<span data-ttu-id="d984e-125">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="d984e-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="d984e-126">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="d984e-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d984e-127">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="d984e-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="d984e-128">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d984e-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d984e-129">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d984e-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d984e-130">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="d984e-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d984e-131">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d984e-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d984e-132">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="d984e-133">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="d984e-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d984e-134">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d984e-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d984e-135">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d984e-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d984e-136">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un locale SAP Business Warehouse, vedere [esempio JSON: copiare i dati da SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d984e-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d984e-137">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooan SAP BW:</span><span class="sxs-lookup"><span data-stu-id="d984e-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d984e-138">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="d984e-138">Linked service properties</span></span>
<span data-ttu-id="d984e-139">Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSAP servizio Business Warehouse (BW) collegati.</span><span class="sxs-lookup"><span data-stu-id="d984e-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="d984e-140">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d984e-140">Property</span></span> | <span data-ttu-id="d984e-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d984e-141">Description</span></span> | <span data-ttu-id="d984e-142">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d984e-142">Allowed values</span></span> | <span data-ttu-id="d984e-143">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="d984e-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="d984e-144">server</span><span class="sxs-lookup"><span data-stu-id="d984e-144">server</span></span> | <span data-ttu-id="d984e-145">Nome del server di hello in SAP BW che hello si trova l'istanza.</span><span class="sxs-lookup"><span data-stu-id="d984e-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="d984e-146">string</span><span class="sxs-lookup"><span data-stu-id="d984e-146">string</span></span> | <span data-ttu-id="d984e-147">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-147">Yes</span></span>
<span data-ttu-id="d984e-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="d984e-148">systemNumber</span></span> | <span data-ttu-id="d984e-149">Numero di sistema di hello sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="d984e-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="d984e-150">Numero decimale a due cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="d984e-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="d984e-151">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-151">Yes</span></span>
<span data-ttu-id="d984e-152">clientId</span><span class="sxs-lookup"><span data-stu-id="d984e-152">clientId</span></span> | <span data-ttu-id="d984e-153">ID client di client hello in hello sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="d984e-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="d984e-154">Numero decimale a tre cifre rappresentato come stringa.</span><span class="sxs-lookup"><span data-stu-id="d984e-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="d984e-155">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-155">Yes</span></span>
<span data-ttu-id="d984e-156">username</span><span class="sxs-lookup"><span data-stu-id="d984e-156">username</span></span> | <span data-ttu-id="d984e-157">Nome dell'utente di hello con server di accesso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="d984e-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="d984e-158">string</span><span class="sxs-lookup"><span data-stu-id="d984e-158">string</span></span> | <span data-ttu-id="d984e-159">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-159">Yes</span></span>
<span data-ttu-id="d984e-160">password</span><span class="sxs-lookup"><span data-stu-id="d984e-160">password</span></span> | <span data-ttu-id="d984e-161">Password utente hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-161">Password for hello user.</span></span> | <span data-ttu-id="d984e-162">string</span><span class="sxs-lookup"><span data-stu-id="d984e-162">string</span></span> | <span data-ttu-id="d984e-163">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-163">Yes</span></span>
<span data-ttu-id="d984e-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d984e-164">gatewayName</span></span> | <span data-ttu-id="d984e-165">Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP BW tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="d984e-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="d984e-166">string</span><span class="sxs-lookup"><span data-stu-id="d984e-166">string</span></span> | <span data-ttu-id="d984e-167">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-167">Yes</span></span>
<span data-ttu-id="d984e-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d984e-168">encryptedCredential</span></span> | <span data-ttu-id="d984e-169">stringa di credenziale crittografato Hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-169">hello encrypted credential string.</span></span> | <span data-ttu-id="d984e-170">string</span><span class="sxs-lookup"><span data-stu-id="d984e-170">string</span></span> | <span data-ttu-id="d984e-171">No</span><span class="sxs-lookup"><span data-stu-id="d984e-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="d984e-172">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="d984e-172">Dataset properties</span></span>
<span data-ttu-id="d984e-173">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d984e-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d984e-174">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="d984e-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d984e-175">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d984e-176">Non esistono proprietà specifiche del tipo supportato per il set di dati di hello SAP BW di tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d984e-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="d984e-177">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="d984e-177">Copy activity properties</span></span>
<span data-ttu-id="d984e-178">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d984e-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d984e-179">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="d984e-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="d984e-180">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="d984e-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d984e-181">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="d984e-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d984e-182">Quando l'origine in attività di copia è di tipo **RelationalSource** (che include SAP BW), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="d984e-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d984e-183">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d984e-183">Property</span></span> | <span data-ttu-id="d984e-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d984e-184">Description</span></span> | <span data-ttu-id="d984e-185">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d984e-185">Allowed values</span></span> | <span data-ttu-id="d984e-186">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d984e-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d984e-187">query</span><span class="sxs-lookup"><span data-stu-id="d984e-187">query</span></span> | <span data-ttu-id="d984e-188">Specifica i dati di tooread query MDX hello dall'istanza di SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="d984e-189">Query MDX.</span><span class="sxs-lookup"><span data-stu-id="d984e-189">MDX query.</span></span> | <span data-ttu-id="d984e-190">Sì</span><span class="sxs-lookup"><span data-stu-id="d984e-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="d984e-191">Esempio JSON: copiare i dati da SAP Business Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d984e-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="d984e-192">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d984e-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d984e-193">Questo esempio viene illustrato come toocopy dati da un tooan SAP Business Warehouse locale archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d984e-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="d984e-194">Tuttavia, i dati possono essere copiati **direttamente** tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d984e-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d984e-195">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="d984e-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="d984e-196">Non include istruzioni dettagliate per la creazione di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="d984e-197">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="d984e-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="d984e-198">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="d984e-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="d984e-199">Un servizio collegato di tipo [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d984e-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="d984e-200">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d984e-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d984e-201">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d984e-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d984e-202">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d984e-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d984e-203">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d984e-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d984e-204">esempio Hello copia dati da un tooan di SAP Business Warehouse istanza blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d984e-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="d984e-205">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d984e-206">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="d984e-207">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d984e-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="d984e-208">Servizio collegato SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="d984e-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="d984e-209">Questo collegato collegamenti al servizio la data factory toohello istanza di SAP BW.</span><span class="sxs-lookup"><span data-stu-id="d984e-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="d984e-210">proprietà tipo Hello è troppo**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="d984e-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="d984e-211">sezione typeProperties Hello fornisce informazioni di connessione per l'istanza di SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="d984e-212">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d984e-212">Azure Storage linked service</span></span>
<span data-ttu-id="d984e-213">Questo collegamento collegamenti al servizio la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d984e-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="d984e-214">proprietà tipo Hello è troppo**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="d984e-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="d984e-215">sezione typeProperties Hello fornisce informazioni di connessione per l'account di archiviazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="d984e-216">Set di dati di input SAP BW</span><span class="sxs-lookup"><span data-stu-id="d984e-216">SAP BW input dataset</span></span>
<span data-ttu-id="d984e-217">Questo set di dati definisce i set di dati SAP Business Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="d984e-218">Impostare il tipo di hello del set di dati Data Factory hello troppo**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d984e-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="d984e-219">mentre per il set di dati SAP BW non è attualmente necessario specificare alcuna proprietà relativa al tipo.</span><span class="sxs-lookup"><span data-stu-id="d984e-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="d984e-220">query Hello nella definizione di attività di copia hello specifica quali tooread dati dall'istanza di SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="d984e-221">L'impostazione di proprietà esterna tootrue informa servizio Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="d984e-222">Frequenza e l'intervallo di proprietà definisce la pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="d984e-223">In questo caso, i dati di hello viene letto dall'istanza di SAP BW hello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d984e-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

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



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d984e-224">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d984e-224">Azure Blob output dataset</span></span>
<span data-ttu-id="d984e-225">Questo set di dati definisce il set di dati di hello output Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d984e-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="d984e-226">proprietà di tipo Hello è tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="d984e-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="d984e-227">Hello typeProperties fornite dove vengono archiviati dati hello copiati dall'istanza di SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="d984e-228">Hello vengono scritti dati tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="d984e-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d984e-229">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="d984e-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d984e-230">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="d984e-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="d984e-231">Pipeline con attività di copia</span><span class="sxs-lookup"><span data-stu-id="d984e-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="d984e-232">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d984e-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d984e-233">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** (per l'origine SAP BW) e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d984e-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d984e-234">query Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="d984e-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="d984e-235">Mapping dei tipi per SAP BW</span><span class="sxs-lookup"><span data-stu-id="d984e-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="d984e-236">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="d984e-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="d984e-237">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="d984e-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="d984e-238">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d984e-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="d984e-239">Quando si spostano dati da SAP BW, hello seguendo i mapping viene utilizzato dai tipi di too.NET tipi SAP BW.</span><span class="sxs-lookup"><span data-stu-id="d984e-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="d984e-240">Tipo di dati nel dizionario ABAP hello</span><span class="sxs-lookup"><span data-stu-id="d984e-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="d984e-241">Tipo di dati .Net</span><span class="sxs-lookup"><span data-stu-id="d984e-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="d984e-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="d984e-242">ACCP</span></span> |  <span data-ttu-id="d984e-243">int</span><span class="sxs-lookup"><span data-stu-id="d984e-243">Int</span></span>
<span data-ttu-id="d984e-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="d984e-244">CHAR</span></span> | <span data-ttu-id="d984e-245">String</span><span class="sxs-lookup"><span data-stu-id="d984e-245">String</span></span>
<span data-ttu-id="d984e-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="d984e-246">CLNT</span></span> | <span data-ttu-id="d984e-247">String</span><span class="sxs-lookup"><span data-stu-id="d984e-247">String</span></span>
<span data-ttu-id="d984e-248">CURR</span><span class="sxs-lookup"><span data-stu-id="d984e-248">CURR</span></span> | <span data-ttu-id="d984e-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="d984e-249">Decimal</span></span>
<span data-ttu-id="d984e-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="d984e-250">CUKY</span></span> | <span data-ttu-id="d984e-251">String</span><span class="sxs-lookup"><span data-stu-id="d984e-251">String</span></span>
<span data-ttu-id="d984e-252">DEC</span><span class="sxs-lookup"><span data-stu-id="d984e-252">DEC</span></span> | <span data-ttu-id="d984e-253">Decimale</span><span class="sxs-lookup"><span data-stu-id="d984e-253">Decimal</span></span>
<span data-ttu-id="d984e-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="d984e-254">FLTP</span></span> | <span data-ttu-id="d984e-255">Double</span><span class="sxs-lookup"><span data-stu-id="d984e-255">Double</span></span>
<span data-ttu-id="d984e-256">INT1</span><span class="sxs-lookup"><span data-stu-id="d984e-256">INT1</span></span> | <span data-ttu-id="d984e-257">Byte</span><span class="sxs-lookup"><span data-stu-id="d984e-257">Byte</span></span>
<span data-ttu-id="d984e-258">INT2</span><span class="sxs-lookup"><span data-stu-id="d984e-258">INT2</span></span> | <span data-ttu-id="d984e-259">Int16</span><span class="sxs-lookup"><span data-stu-id="d984e-259">Int16</span></span>
<span data-ttu-id="d984e-260">INT4</span><span class="sxs-lookup"><span data-stu-id="d984e-260">INT4</span></span> | <span data-ttu-id="d984e-261">int</span><span class="sxs-lookup"><span data-stu-id="d984e-261">Int</span></span>
<span data-ttu-id="d984e-262">LANG</span><span class="sxs-lookup"><span data-stu-id="d984e-262">LANG</span></span> | <span data-ttu-id="d984e-263">String</span><span class="sxs-lookup"><span data-stu-id="d984e-263">String</span></span>
<span data-ttu-id="d984e-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="d984e-264">LCHR</span></span> | <span data-ttu-id="d984e-265">String</span><span class="sxs-lookup"><span data-stu-id="d984e-265">String</span></span>
<span data-ttu-id="d984e-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="d984e-266">LRAW</span></span> | <span data-ttu-id="d984e-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d984e-267">Byte[]</span></span>
<span data-ttu-id="d984e-268">PREC</span><span class="sxs-lookup"><span data-stu-id="d984e-268">PREC</span></span> | <span data-ttu-id="d984e-269">Int16</span><span class="sxs-lookup"><span data-stu-id="d984e-269">Int16</span></span>
<span data-ttu-id="d984e-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="d984e-270">QUAN</span></span> | <span data-ttu-id="d984e-271">Decimale</span><span class="sxs-lookup"><span data-stu-id="d984e-271">Decimal</span></span>
<span data-ttu-id="d984e-272">RAW</span><span class="sxs-lookup"><span data-stu-id="d984e-272">RAW</span></span> | <span data-ttu-id="d984e-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d984e-273">Byte[]</span></span>
<span data-ttu-id="d984e-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="d984e-274">RAWSTRING</span></span> | <span data-ttu-id="d984e-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d984e-275">Byte[]</span></span>
<span data-ttu-id="d984e-276">STRING</span><span class="sxs-lookup"><span data-stu-id="d984e-276">STRING</span></span> | <span data-ttu-id="d984e-277">String</span><span class="sxs-lookup"><span data-stu-id="d984e-277">String</span></span>
<span data-ttu-id="d984e-278">UNITÀ</span><span class="sxs-lookup"><span data-stu-id="d984e-278">UNIT</span></span> | <span data-ttu-id="d984e-279">String</span><span class="sxs-lookup"><span data-stu-id="d984e-279">String</span></span>
<span data-ttu-id="d984e-280">DATS</span><span class="sxs-lookup"><span data-stu-id="d984e-280">DATS</span></span> | <span data-ttu-id="d984e-281">String</span><span class="sxs-lookup"><span data-stu-id="d984e-281">String</span></span>
<span data-ttu-id="d984e-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="d984e-282">NUMC</span></span> | <span data-ttu-id="d984e-283">String</span><span class="sxs-lookup"><span data-stu-id="d984e-283">String</span></span>
<span data-ttu-id="d984e-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="d984e-284">TIMS</span></span> | <span data-ttu-id="d984e-285">String</span><span class="sxs-lookup"><span data-stu-id="d984e-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="d984e-286">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d984e-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="d984e-287">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="d984e-287">Map source toosink columns</span></span>
<span data-ttu-id="d984e-288">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d984e-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d984e-289">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="d984e-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="d984e-290">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="d984e-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="d984e-291">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="d984e-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d984e-292">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="d984e-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d984e-293">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="d984e-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d984e-294">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="d984e-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d984e-295">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d984e-295">Performance and Tuning</span></span>
<span data-ttu-id="d984e-296">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="d984e-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
