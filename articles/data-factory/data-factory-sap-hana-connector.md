---
title: aaaMove dati da SAP HANA utilizzando Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da SAP HANA usando Azure Data Factory.
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
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="b075a-103">Spostare dati da SAP HANA usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b075a-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="b075a-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="b075a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="b075a-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="b075a-106">È possibile copiare dati da un archivio di dati di on-premise SAP HANA dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="b075a-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="b075a-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="b075a-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b075a-108">Data factory di supporta attualmente solo lo spostamento di archivi di dati da un tooother SAP HANA, ma non per lo spostamento dei dati da altri dati archivia tooan SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b075a-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="b075a-109">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="b075a-109">Supported versions and installation</span></span>
<span data-ttu-id="b075a-110">Questo connettore supporta qualsiasi versione del database SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b075a-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="b075a-111">Supporta anche la copia di dati da modelli di informazioni HANA (ad esempio, dalle viste di analisi e calcolo) e da tabelle Riga/Colonna tramite query SQL.</span><span class="sxs-lookup"><span data-stu-id="b075a-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="b075a-112">tooenable hello connettività toohello istanza SAP HANA, installare hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="b075a-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="b075a-113">**Gateway di gestione dati**: servizio di Data Factory supporta la connessione dati locali tooon archivi (incluso SAP HANA) utilizzando un componente chiamato Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="b075a-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="b075a-114">toolearn sul Gateway di gestione dati e istruzioni dettagliate per la configurazione di gateway di hello, vedere [dati di spostamento tra i dati locali toocloud archiviano dati](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b075a-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="b075a-115">Gateway è necessario anche se hello SAP HANA è ospitato in una macchina virtuale IaaS di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="b075a-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="b075a-116">È possibile installare il gateway di hello in hello stessa macchina virtuale come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="b075a-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="b075a-117">**Il driver ODBC di SAP HANA** nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="b075a-118">È possibile scaricare i driver ODBC di SAP HANA hello da hello [area Download di Software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="b075a-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="b075a-119">Ricerca con la parola chiave hello **SAP HANA CLIENT per Windows**.</span><span class="sxs-lookup"><span data-stu-id="b075a-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="b075a-120">introduttiva</span><span class="sxs-lookup"><span data-stu-id="b075a-120">Getting started</span></span>
<span data-ttu-id="b075a-121">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="b075a-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="b075a-122">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="b075a-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b075a-123">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="b075a-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="b075a-124">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="b075a-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b075a-125">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="b075a-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b075a-126">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="b075a-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b075a-127">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="b075a-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="b075a-128">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="b075a-129">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="b075a-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b075a-130">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="b075a-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="b075a-131">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b075a-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="b075a-132">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un SAP HANA locale, vedere [esempio JSON: copiare i dati da SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b075a-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="b075a-133">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooan SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="b075a-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b075a-134">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="b075a-134">Linked service properties</span></span>
<span data-ttu-id="b075a-135">Hello nella tabella seguente fornisce una descrizione per JSON elementi specifici tooSAP HANA servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="b075a-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="b075a-136">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b075a-136">Property</span></span> | <span data-ttu-id="b075a-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b075a-137">Description</span></span> | <span data-ttu-id="b075a-138">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="b075a-138">Allowed values</span></span> | <span data-ttu-id="b075a-139">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="b075a-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="b075a-140">server</span><span class="sxs-lookup"><span data-stu-id="b075a-140">server</span></span> | <span data-ttu-id="b075a-141">Nome del server di hello in SAP HANA quali hello si trova l'istanza.</span><span class="sxs-lookup"><span data-stu-id="b075a-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="b075a-142">Se il server usa una porta personalizzata, specificare `server:port`.</span><span class="sxs-lookup"><span data-stu-id="b075a-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="b075a-143">string</span><span class="sxs-lookup"><span data-stu-id="b075a-143">string</span></span> | <span data-ttu-id="b075a-144">Sì</span><span class="sxs-lookup"><span data-stu-id="b075a-144">Yes</span></span>
<span data-ttu-id="b075a-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b075a-145">authenticationType</span></span> | <span data-ttu-id="b075a-146">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b075a-146">Type of authentication.</span></span> | <span data-ttu-id="b075a-147">string.</span><span class="sxs-lookup"><span data-stu-id="b075a-147">string.</span></span> <span data-ttu-id="b075a-148">"Basic" o "Windows"</span><span class="sxs-lookup"><span data-stu-id="b075a-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="b075a-149">Sì</span><span class="sxs-lookup"><span data-stu-id="b075a-149">Yes</span></span> 
<span data-ttu-id="b075a-150">username</span><span class="sxs-lookup"><span data-stu-id="b075a-150">username</span></span> | <span data-ttu-id="b075a-151">Nome dell'utente di hello con server di accesso toohello SAP</span><span class="sxs-lookup"><span data-stu-id="b075a-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="b075a-152">string</span><span class="sxs-lookup"><span data-stu-id="b075a-152">string</span></span> | <span data-ttu-id="b075a-153">Sì</span><span class="sxs-lookup"><span data-stu-id="b075a-153">Yes</span></span>
<span data-ttu-id="b075a-154">password</span><span class="sxs-lookup"><span data-stu-id="b075a-154">password</span></span> | <span data-ttu-id="b075a-155">Password utente hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-155">Password for hello user.</span></span> | <span data-ttu-id="b075a-156">string</span><span class="sxs-lookup"><span data-stu-id="b075a-156">string</span></span> | <span data-ttu-id="b075a-157">Sì</span><span class="sxs-lookup"><span data-stu-id="b075a-157">Yes</span></span>
<span data-ttu-id="b075a-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b075a-158">gatewayName</span></span> | <span data-ttu-id="b075a-159">Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP HANA tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="b075a-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="b075a-160">string</span><span class="sxs-lookup"><span data-stu-id="b075a-160">string</span></span> | <span data-ttu-id="b075a-161">Sì</span><span class="sxs-lookup"><span data-stu-id="b075a-161">Yes</span></span>
<span data-ttu-id="b075a-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="b075a-162">encryptedCredential</span></span> | <span data-ttu-id="b075a-163">stringa di credenziale crittografato Hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-163">hello encrypted credential string.</span></span> | <span data-ttu-id="b075a-164">string</span><span class="sxs-lookup"><span data-stu-id="b075a-164">string</span></span> | <span data-ttu-id="b075a-165">No</span><span class="sxs-lookup"><span data-stu-id="b075a-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="b075a-166">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="b075a-166">Dataset properties</span></span>
<span data-ttu-id="b075a-167">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b075a-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b075a-168">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="b075a-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b075a-169">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b075a-170">Non esistono proprietà specifiche del tipo supportato per i set di dati SAP HANA hello di tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="b075a-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="b075a-171">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="b075a-171">Copy activity properties</span></span>
<span data-ttu-id="b075a-172">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b075a-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b075a-173">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="b075a-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="b075a-174">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="b075a-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="b075a-175">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="b075a-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="b075a-176">Quando l'origine in attività di copia è di tipo **RelationalSource** (che include SAP HANA), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="b075a-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="b075a-177">Proprietà</span><span class="sxs-lookup"><span data-stu-id="b075a-177">Property</span></span> | <span data-ttu-id="b075a-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b075a-178">Description</span></span> | <span data-ttu-id="b075a-179">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="b075a-179">Allowed values</span></span> | <span data-ttu-id="b075a-180">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b075a-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b075a-181">query</span><span class="sxs-lookup"><span data-stu-id="b075a-181">query</span></span> | <span data-ttu-id="b075a-182">Specifica i dati di tooread query SQL hello dall'istanza di SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="b075a-183">Query SQL.</span><span class="sxs-lookup"><span data-stu-id="b075a-183">SQL query.</span></span> | <span data-ttu-id="b075a-184">Sì</span><span class="sxs-lookup"><span data-stu-id="b075a-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="b075a-185">Esempio JSON: copiare i dati da SAP HANA tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="b075a-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="b075a-186">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b075a-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b075a-187">Questo esempio viene illustrato come toocopy dati da un tooan di SAP HANA locale archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b075a-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="b075a-188">Tuttavia, i dati possono essere copiati **direttamente** tooany di sink hello elencati [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b075a-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="b075a-189">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="b075a-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="b075a-190">Non include istruzioni dettagliate per la creazione di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="b075a-191">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="b075a-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="b075a-192">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="b075a-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="b075a-193">Un servizio collegato di tipo [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b075a-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="b075a-194">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b075a-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b075a-195">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b075a-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b075a-196">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b075a-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b075a-197">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b075a-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b075a-198">esempio Hello copia dati da un tooan di SAP HANA istanza blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b075a-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="b075a-199">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="b075a-200">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="b075a-201">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b075a-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="b075a-202">Servizio collegato SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b075a-202">SAP HANA linked service</span></span>
<span data-ttu-id="b075a-203">Questo collegato collegamenti al servizio la data factory toohello istanza di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b075a-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="b075a-204">proprietà tipo Hello è troppo**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="b075a-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="b075a-205">sezione typeProperties Hello fornisce informazioni di connessione per l'istanza di SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="b075a-206">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b075a-206">Azure Storage linked service</span></span>
<span data-ttu-id="b075a-207">Questo collegamento collegamenti al servizio la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b075a-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="b075a-208">proprietà tipo Hello è troppo**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="b075a-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="b075a-209">sezione typeProperties Hello fornisce informazioni di connessione per l'account di archiviazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="b075a-210">Set di dati input di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b075a-210">SAP HANA input dataset</span></span>

<span data-ttu-id="b075a-211">Questo set di dati definisce i set di dati SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="b075a-212">Impostare il tipo di hello del set di dati Data Factory hello troppo**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="b075a-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="b075a-213">mentre per il set di dati SAP HANA non è attualmente necessario specificare alcuna proprietà relativa al tipo.</span><span class="sxs-lookup"><span data-stu-id="b075a-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="b075a-214">query Hello nella definizione di attività di copia hello specifica quali tooread dati dall'istanza di SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="b075a-215">L'impostazione di proprietà esterna tootrue informa servizio Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="b075a-216">Frequenza e l'intervallo di proprietà definisce la pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="b075a-217">In questo caso, i dati di hello viene letto dall'istanza di SAP HANA hello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b075a-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="b075a-218">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b075a-218">Azure Blob output dataset</span></span>
<span data-ttu-id="b075a-219">Questo set di dati definisce il set di dati di hello output Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b075a-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="b075a-220">proprietà di tipo Hello è tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="b075a-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="b075a-221">Hello typeProperties fornite dove vengono archiviati dati hello copiati dall'istanza di SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="b075a-222">Hello vengono scritti dati tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="b075a-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b075a-223">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="b075a-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b075a-224">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="b075a-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="b075a-225">Pipeline con attività di copia</span><span class="sxs-lookup"><span data-stu-id="b075a-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="b075a-226">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b075a-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="b075a-227">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** (per l'origine di SAP HANA) e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b075a-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="b075a-228">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="b075a-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="b075a-229">Mapping dei tipi per SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b075a-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="b075a-230">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="b075a-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="b075a-231">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="b075a-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="b075a-232">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="b075a-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="b075a-233">Quando si spostano dati da SAP HANA, hello seguendo i mapping viene utilizzato dai tipi too.NET tipi di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="b075a-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="b075a-234">Tipo SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b075a-234">SAP HANA Type</span></span> | <span data-ttu-id="b075a-235">Tipo basato su .Net</span><span class="sxs-lookup"><span data-stu-id="b075a-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="b075a-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="b075a-236">TINYINT</span></span> | <span data-ttu-id="b075a-237">Byte</span><span class="sxs-lookup"><span data-stu-id="b075a-237">Byte</span></span>
<span data-ttu-id="b075a-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="b075a-238">SMALLINT</span></span> | <span data-ttu-id="b075a-239">Int16</span><span class="sxs-lookup"><span data-stu-id="b075a-239">Int16</span></span>
<span data-ttu-id="b075a-240">INT</span><span class="sxs-lookup"><span data-stu-id="b075a-240">INT</span></span> | <span data-ttu-id="b075a-241">Int32</span><span class="sxs-lookup"><span data-stu-id="b075a-241">Int32</span></span>
<span data-ttu-id="b075a-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="b075a-242">BIGINT</span></span> | <span data-ttu-id="b075a-243">Int64</span><span class="sxs-lookup"><span data-stu-id="b075a-243">Int64</span></span>
<span data-ttu-id="b075a-244">REAL</span><span class="sxs-lookup"><span data-stu-id="b075a-244">REAL</span></span> | <span data-ttu-id="b075a-245">Single</span><span class="sxs-lookup"><span data-stu-id="b075a-245">Single</span></span>
<span data-ttu-id="b075a-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="b075a-246">DOUBLE</span></span> | <span data-ttu-id="b075a-247">Single</span><span class="sxs-lookup"><span data-stu-id="b075a-247">Single</span></span>
<span data-ttu-id="b075a-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="b075a-248">DECIMAL</span></span> | <span data-ttu-id="b075a-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="b075a-249">Decimal</span></span>
<span data-ttu-id="b075a-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="b075a-250">BOOLEAN</span></span> | <span data-ttu-id="b075a-251">Byte</span><span class="sxs-lookup"><span data-stu-id="b075a-251">Byte</span></span>
<span data-ttu-id="b075a-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="b075a-252">VARCHAR</span></span> | <span data-ttu-id="b075a-253">String</span><span class="sxs-lookup"><span data-stu-id="b075a-253">String</span></span>
<span data-ttu-id="b075a-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="b075a-254">NVARCHAR</span></span> | <span data-ttu-id="b075a-255">String</span><span class="sxs-lookup"><span data-stu-id="b075a-255">String</span></span>
<span data-ttu-id="b075a-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="b075a-256">CLOB</span></span> | <span data-ttu-id="b075a-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b075a-257">Byte[]</span></span>
<span data-ttu-id="b075a-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="b075a-258">ALPHANUM</span></span> | <span data-ttu-id="b075a-259">String</span><span class="sxs-lookup"><span data-stu-id="b075a-259">String</span></span>
<span data-ttu-id="b075a-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="b075a-260">BLOB</span></span> | <span data-ttu-id="b075a-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b075a-261">Byte[]</span></span>
<span data-ttu-id="b075a-262">DATE</span><span class="sxs-lookup"><span data-stu-id="b075a-262">DATE</span></span> | <span data-ttu-id="b075a-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="b075a-263">DateTime</span></span>
<span data-ttu-id="b075a-264">TIME</span><span class="sxs-lookup"><span data-stu-id="b075a-264">TIME</span></span> | <span data-ttu-id="b075a-265">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="b075a-265">TimeSpan</span></span>
<span data-ttu-id="b075a-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="b075a-266">TIMESTAMP</span></span> | <span data-ttu-id="b075a-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="b075a-267">DateTime</span></span>
<span data-ttu-id="b075a-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="b075a-268">SECONDDATE</span></span> | <span data-ttu-id="b075a-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="b075a-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="b075a-270">Limitazioni note</span><span class="sxs-lookup"><span data-stu-id="b075a-270">Known limitations</span></span>
<span data-ttu-id="b075a-271">Quando si copiano dati da SAP HANA, è necessario tenere conto di alcune limitazioni:</span><span class="sxs-lookup"><span data-stu-id="b075a-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="b075a-272">Le stringhe NVARCHAR vengono troncate toomaximum lunghezza di 4000 caratteri Unicode</span><span class="sxs-lookup"><span data-stu-id="b075a-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="b075a-273">SMALLDECIMAL non è supportato</span><span class="sxs-lookup"><span data-stu-id="b075a-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="b075a-274">VARBINARY non è supportato</span><span class="sxs-lookup"><span data-stu-id="b075a-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="b075a-275">Le date valide sono tra comprese tra il 30/12/1899 e il 31/12/9999</span><span class="sxs-lookup"><span data-stu-id="b075a-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="b075a-276">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="b075a-276">Map source toosink columns</span></span>
<span data-ttu-id="b075a-277">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b075a-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="b075a-278">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="b075a-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="b075a-279">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="b075a-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="b075a-280">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="b075a-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b075a-281">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="b075a-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b075a-282">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="b075a-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b075a-283">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="b075a-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b075a-284">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b075a-284">Performance and Tuning</span></span>
<span data-ttu-id="b075a-285">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="b075a-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
