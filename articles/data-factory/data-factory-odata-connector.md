---
title: aaaMove dati da origini di OData | Documenti Microsoft
description: Informazioni su come origini dei dati toomove da OData usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="df820-103">Spostare i dati da un'origine OData usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="df820-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="df820-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un'origine OData.</span><span class="sxs-lookup"><span data-stu-id="df820-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="df820-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="df820-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="df820-106">È possibile copiare dati da un archivio di dati OData origine tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="df820-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="df820-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="df820-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="df820-108">Data factory di supporta attualmente solo lo spostamento di archivi di dati da dati tooother origine OData, ma non per lo spostamento dei dati da altri dati di origine OData tooan Archivia.</span><span class="sxs-lookup"><span data-stu-id="df820-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="df820-109">Versioni supportate e tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="df820-109">Supported versions and authentication types</span></span>
<span data-ttu-id="df820-110">Questo connettore OData supporta OData versione 3.0 e 4.0 e la copia dei dati dalle origini OData cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="df820-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="df820-111">Per hello quest'ultimo, è necessario tooinstall hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="df820-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="df820-112">Vedere l’articolo [Spostare dati tra cloud e locale](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sui Gateway di Gestione dati.</span><span class="sxs-lookup"><span data-stu-id="df820-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="df820-113">Sono supportati i tipi di autenticazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="df820-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="df820-114">tooaccess **cloud** feed OData, è possibile utilizzare anonima, base (nome utente e password) o Azure Active Directory basato su autenticazione OAuth.</span><span class="sxs-lookup"><span data-stu-id="df820-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="df820-115">tooaccess **locale** feed OData, è possibile usare anonima, base (nome utente e password), o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="df820-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="df820-116">introduttiva</span><span class="sxs-lookup"><span data-stu-id="df820-116">Getting started</span></span>
<span data-ttu-id="df820-117">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine OData usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="df820-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="df820-118">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="df820-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="df820-119">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="df820-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="df820-120">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="df820-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="df820-121">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="df820-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="df820-122">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="df820-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="df820-123">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="df820-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="df820-124">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="df820-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="df820-125">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="df820-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="df820-126">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="df820-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="df820-127">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df820-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="df820-128">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un'origine OData, vedere [esempio JSON: copiare i dati da tooAzure origine OData Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="df820-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="df820-129">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono utilizzati toodefine Data Factory entità specifiche tooOData origine:</span><span class="sxs-lookup"><span data-stu-id="df820-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="df820-130">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="df820-130">Linked Service properties</span></span>
<span data-ttu-id="df820-131">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooOData collegato gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="df820-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="df820-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="df820-132">Property</span></span> | <span data-ttu-id="df820-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df820-133">Description</span></span> | <span data-ttu-id="df820-134">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="df820-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df820-135">type</span><span class="sxs-lookup"><span data-stu-id="df820-135">type</span></span> |<span data-ttu-id="df820-136">proprietà di tipo Hello deve essere impostata su: **OData**</span><span class="sxs-lookup"><span data-stu-id="df820-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="df820-137">Sì</span><span class="sxs-lookup"><span data-stu-id="df820-137">Yes</span></span> |
| <span data-ttu-id="df820-138">URL</span><span class="sxs-lookup"><span data-stu-id="df820-138">url</span></span> |<span data-ttu-id="df820-139">URL del servizio OData hello.</span><span class="sxs-lookup"><span data-stu-id="df820-139">Url of hello OData service.</span></span> |<span data-ttu-id="df820-140">Sì</span><span class="sxs-lookup"><span data-stu-id="df820-140">Yes</span></span> |
| <span data-ttu-id="df820-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="df820-141">authenticationType</span></span> |<span data-ttu-id="df820-142">Tipo di autenticazione usato tooconnect toohello un'origine OData.</span><span class="sxs-lookup"><span data-stu-id="df820-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="df820-143">Per OData in cloud, i valori possibili sono Anonymous, Basic e OAuth. Si noti che Azure Data Factory attualmente supporta solo OAuth basato su Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="df820-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="df820-144">Per OData locale, i valori possibili sono Anonima, Di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="df820-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="df820-145">Sì</span><span class="sxs-lookup"><span data-stu-id="df820-145">Yes</span></span> |
| <span data-ttu-id="df820-146">username</span><span class="sxs-lookup"><span data-stu-id="df820-146">username</span></span> |<span data-ttu-id="df820-147">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="df820-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="df820-148">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="df820-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="df820-149">password</span><span class="sxs-lookup"><span data-stu-id="df820-149">password</span></span> |<span data-ttu-id="df820-150">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="df820-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="df820-151">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="df820-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="df820-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="df820-152">authorizedCredential</span></span> |<span data-ttu-id="df820-153">Se si utilizza OAuth, fare clic su **Authorize** pulsante nell'Editor o hello Data Factory Copia guidata e immettere le credenziali, il valore di hello di questa proprietà verrà generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="df820-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="df820-154">Sì (solo se si usa l'autenticazione OAuth)</span><span class="sxs-lookup"><span data-stu-id="df820-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="df820-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="df820-155">gatewayName</span></span> |<span data-ttu-id="df820-156">Nome del gateway hello hello servizio Data Factory deve usare servizio OData di tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="df820-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="df820-157">Specificare solo se si copiano dati da un'origine OData locale.</span><span class="sxs-lookup"><span data-stu-id="df820-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="df820-158">No</span><span class="sxs-lookup"><span data-stu-id="df820-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="df820-159">Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="df820-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="df820-160">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="df820-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="df820-161">Uso dell'autenticazione di Windows per accedere all'origine OData locale</span><span class="sxs-lookup"><span data-stu-id="df820-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="df820-162">Uso dell'autenticazione OAuth per accedere all'origine OData cloud</span><span class="sxs-lookup"><span data-stu-id="df820-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="df820-163">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="df820-163">Dataset properties</span></span>
<span data-ttu-id="df820-164">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="df820-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="df820-165">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="df820-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="df820-166">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="df820-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="df820-167">sezione Hello typeProperties per set di dati di tipo **ODataResource** (che include set di dati OData) è hello seguenti proprietà</span><span class="sxs-lookup"><span data-stu-id="df820-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="df820-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="df820-168">Property</span></span> | <span data-ttu-id="df820-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df820-169">Description</span></span> | <span data-ttu-id="df820-170">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="df820-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df820-171">path</span><span class="sxs-lookup"><span data-stu-id="df820-171">path</span></span> |<span data-ttu-id="df820-172">Percorso toohello risorse OData</span><span class="sxs-lookup"><span data-stu-id="df820-172">Path toohello OData resource</span></span> |<span data-ttu-id="df820-173">No</span><span class="sxs-lookup"><span data-stu-id="df820-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="df820-174">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="df820-174">Copy activity properties</span></span>
<span data-ttu-id="df820-175">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="df820-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="df820-176">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="df820-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="df820-177">Le proprietà disponibili nella sezione typeProperties hello di attività hello hello invece variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="df820-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="df820-178">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="df820-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="df820-179">Quando l'origine è di tipo **RelationalSource** (che include OData) hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="df820-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="df820-180">Proprietà</span><span class="sxs-lookup"><span data-stu-id="df820-180">Property</span></span> | <span data-ttu-id="df820-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df820-181">Description</span></span> | <span data-ttu-id="df820-182">Esempio</span><span class="sxs-lookup"><span data-stu-id="df820-182">Example</span></span> | <span data-ttu-id="df820-183">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="df820-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df820-184">query</span><span class="sxs-lookup"><span data-stu-id="df820-184">query</span></span> |<span data-ttu-id="df820-185">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="df820-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="df820-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="df820-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="df820-187">No</span><span class="sxs-lookup"><span data-stu-id="df820-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="df820-188">Mapping dei tipi per OData</span><span class="sxs-lookup"><span data-stu-id="df820-188">Type Mapping for OData</span></span>
<span data-ttu-id="df820-189">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="df820-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="df820-190">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="df820-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="df820-191">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="df820-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="df820-192">Quando si spostano dati da OData, hello mapping seguenti vengono utilizzati dal tipo di too.NET tipi OData.</span><span class="sxs-lookup"><span data-stu-id="df820-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="df820-193">Tipo di dati OData</span><span class="sxs-lookup"><span data-stu-id="df820-193">OData Data Type</span></span> | <span data-ttu-id="df820-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="df820-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="df820-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="df820-195">Edm.Binary</span></span> |<span data-ttu-id="df820-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="df820-196">Byte[]</span></span> |
| <span data-ttu-id="df820-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="df820-197">Edm.Boolean</span></span> |<span data-ttu-id="df820-198">Booleano</span><span class="sxs-lookup"><span data-stu-id="df820-198">Bool</span></span> |
| <span data-ttu-id="df820-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="df820-199">Edm.Byte</span></span> |<span data-ttu-id="df820-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="df820-200">Byte[]</span></span> |
| <span data-ttu-id="df820-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="df820-201">Edm.DateTime</span></span> |<span data-ttu-id="df820-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="df820-202">DateTime</span></span> |
| <span data-ttu-id="df820-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="df820-203">Edm.Decimal</span></span> |<span data-ttu-id="df820-204">Decimale</span><span class="sxs-lookup"><span data-stu-id="df820-204">Decimal</span></span> |
| <span data-ttu-id="df820-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="df820-205">Edm.Double</span></span> |<span data-ttu-id="df820-206">Double</span><span class="sxs-lookup"><span data-stu-id="df820-206">Double</span></span> |
| <span data-ttu-id="df820-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="df820-207">Edm.Single</span></span> |<span data-ttu-id="df820-208">Single</span><span class="sxs-lookup"><span data-stu-id="df820-208">Single</span></span> |
| <span data-ttu-id="df820-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="df820-209">Edm.Guid</span></span> |<span data-ttu-id="df820-210">Guid</span><span class="sxs-lookup"><span data-stu-id="df820-210">Guid</span></span> |
| <span data-ttu-id="df820-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="df820-211">Edm.Int16</span></span> |<span data-ttu-id="df820-212">Int16</span><span class="sxs-lookup"><span data-stu-id="df820-212">Int16</span></span> |
| <span data-ttu-id="df820-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="df820-213">Edm.Int32</span></span> |<span data-ttu-id="df820-214">Int32</span><span class="sxs-lookup"><span data-stu-id="df820-214">Int32</span></span> |
| <span data-ttu-id="df820-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="df820-215">Edm.Int64</span></span> |<span data-ttu-id="df820-216">Int64</span><span class="sxs-lookup"><span data-stu-id="df820-216">Int64</span></span> |
| <span data-ttu-id="df820-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="df820-217">Edm.SByte</span></span> |<span data-ttu-id="df820-218">Int16</span><span class="sxs-lookup"><span data-stu-id="df820-218">Int16</span></span> |
| <span data-ttu-id="df820-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="df820-219">Edm.String</span></span> |<span data-ttu-id="df820-220">String</span><span class="sxs-lookup"><span data-stu-id="df820-220">String</span></span> |
| <span data-ttu-id="df820-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="df820-221">Edm.Time</span></span> |<span data-ttu-id="df820-222">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="df820-222">TimeSpan</span></span> |
| <span data-ttu-id="df820-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="df820-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="df820-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="df820-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="df820-225">Tipi di dati OData complessi. Gli oggetti, ad esempio, non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="df820-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="df820-226">Esempio JSON: copiare i dati da tooAzure origine OData Blob</span><span class="sxs-lookup"><span data-stu-id="df820-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="df820-227">In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="df820-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="df820-228">Visualizzano come origine dei dati di toocopy da OData tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="df820-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="df820-229">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="df820-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="df820-230">esempio Hello è hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="df820-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="df820-231">Un servizio collegato di tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="df820-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="df820-232">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="df820-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="df820-233">Un [set di dati](data-factory-create-datasets.md) di input di tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="df820-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="df820-234">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="df820-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="df820-235">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="df820-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="df820-236">esempio Hello copia dati da una query su un tooan origine OData blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="df820-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="df820-237">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="df820-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="df820-238">**Servizio collegato di OData:** in questo esempio viene utilizzata l'autenticazione anonima di hello.</span><span class="sxs-lookup"><span data-stu-id="df820-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="df820-239">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato OData](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="df820-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="df820-240">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="df820-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="df820-241">**Set di dati di input OData:**</span><span class="sxs-lookup"><span data-stu-id="df820-241">**OData input dataset:**</span></span>

<span data-ttu-id="df820-242">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="df820-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="df820-243">Specifica di **percorso** nel set di dati hello definizione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="df820-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="df820-244">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="df820-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="df820-245">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="df820-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="df820-246">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="df820-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="df820-247">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="df820-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="df820-248">**Attività di copia in una pipeline con un'origine OData e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="df820-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="df820-249">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="df820-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="df820-250">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="df820-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="df820-251">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati (il più recente) più recenti hello dall'origine OData hello.</span><span class="sxs-lookup"><span data-stu-id="df820-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="df820-252">Specifica di **query** nella pipeline hello definizione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="df820-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="df820-253">Hello **URL** è che il servizio di Data Factory hello utilizza dati tooretrieve: l'URL specificato nel hello servizio collegato (obbligatorio) + percorso specificato nel set di dati hello (facoltativo) + eseguire una query nella pipeline di hello (facoltativa).</span><span class="sxs-lookup"><span data-stu-id="df820-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="df820-254">Mapping dei tipi per OData</span><span class="sxs-lookup"><span data-stu-id="df820-254">Type mapping for OData</span></span>
<span data-ttu-id="df820-255">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="df820-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="df820-256">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="df820-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="df820-257">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="df820-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="df820-258">Quando si spostano dati da archivi dati OData, tipi di dati OData sono tipi too.NET mappato.</span><span class="sxs-lookup"><span data-stu-id="df820-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="df820-259">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="df820-259">Map source toosink columns</span></span>
<span data-ttu-id="df820-260">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="df820-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="df820-261">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="df820-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="df820-262">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="df820-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="df820-263">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="df820-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="df820-264">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="df820-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="df820-265">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="df820-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="df820-266">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="df820-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="df820-267">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="df820-267">Performance and Tuning</span></span>
<span data-ttu-id="df820-268">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="df820-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
