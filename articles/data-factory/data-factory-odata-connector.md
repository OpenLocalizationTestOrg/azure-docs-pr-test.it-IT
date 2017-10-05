---
title: Spostare dati da origini OData | Documentazione Microsoft
description: Informazioni su come spostare i dati da origini OData usando Azure Data Factory.
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
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="add6e-103">Spostare i dati da un'origine OData usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="add6e-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="add6e-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un'origine OData.</span><span class="sxs-lookup"><span data-stu-id="add6e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="add6e-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="add6e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="add6e-106">È possibile copiare dati da un'origine OData a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="add6e-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="add6e-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="add6e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="add6e-108">Data Factory supporta attualmente solo lo spostamento dei dati da un'origine OData ad altri archivi dati, non da altri archivi dati a un'origine OData.</span><span class="sxs-lookup"><span data-stu-id="add6e-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="add6e-109">Versioni supportate e tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="add6e-109">Supported versions and authentication types</span></span>
<span data-ttu-id="add6e-110">Questo connettore OData supporta OData versione 3.0 e 4.0 e la copia dei dati dalle origini OData cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="add6e-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="add6e-111">Nel secondo caso, è necessario installare il gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="add6e-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="add6e-112">Vedere l’articolo [Spostare dati tra cloud e locale](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sui Gateway di Gestione dati.</span><span class="sxs-lookup"><span data-stu-id="add6e-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="add6e-113">Sono supportati i tipi di autenticazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="add6e-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="add6e-114">Per accedere al feed OData **cloud**, è possibile usare l'autenticazione anonima, di base (nome utente e password) o l'autenticazione OAuth basata su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="add6e-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="add6e-115">Per accedere al feed OData **locale**, è possibile usare l'autenticazione anonima, di base (nome utente e password) o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="add6e-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="add6e-116">Introduzione</span><span class="sxs-lookup"><span data-stu-id="add6e-116">Getting started</span></span>
<span data-ttu-id="add6e-117">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine OData usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="add6e-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="add6e-118">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="add6e-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="add6e-119">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="add6e-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="add6e-120">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="add6e-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="add6e-121">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="add6e-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="add6e-122">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="add6e-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="add6e-123">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="add6e-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="add6e-124">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="add6e-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="add6e-125">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="add6e-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="add6e-126">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="add6e-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="add6e-127">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="add6e-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="add6e-128">Per un esempio con definizioni JSON per entità di data factory utilizzate per copiare dati da un'origine OData, vedere la sezione [Esempio JSON: Copiare dati da un'origine OData al BLOB di Azure](#json-example-copy-data-from-odata-source-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="add6e-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="add6e-129">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche dell'origine OData:</span><span class="sxs-lookup"><span data-stu-id="add6e-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="add6e-130">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="add6e-130">Linked Service properties</span></span>
<span data-ttu-id="add6e-131">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato OData.</span><span class="sxs-lookup"><span data-stu-id="add6e-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="add6e-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="add6e-132">Property</span></span> | <span data-ttu-id="add6e-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="add6e-133">Description</span></span> | <span data-ttu-id="add6e-134">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="add6e-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="add6e-135">type</span><span class="sxs-lookup"><span data-stu-id="add6e-135">type</span></span> |<span data-ttu-id="add6e-136">La proprietà type deve essere impostata su: **OData**</span><span class="sxs-lookup"><span data-stu-id="add6e-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="add6e-137">Sì</span><span class="sxs-lookup"><span data-stu-id="add6e-137">Yes</span></span> |
| <span data-ttu-id="add6e-138">URL</span><span class="sxs-lookup"><span data-stu-id="add6e-138">url</span></span> |<span data-ttu-id="add6e-139">URL del servizio OData.</span><span class="sxs-lookup"><span data-stu-id="add6e-139">Url of the OData service.</span></span> |<span data-ttu-id="add6e-140">Sì</span><span class="sxs-lookup"><span data-stu-id="add6e-140">Yes</span></span> |
| <span data-ttu-id="add6e-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="add6e-141">authenticationType</span></span> |<span data-ttu-id="add6e-142">Tipo di autenticazione usato per connettersi all'origine OData.</span><span class="sxs-lookup"><span data-stu-id="add6e-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="add6e-143">Per OData in cloud, i valori possibili sono Anonymous, Basic e OAuth. Si noti che Azure Data Factory attualmente supporta solo OAuth basato su Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="add6e-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="add6e-144">Per OData locale, i valori possibili sono Anonima, Di base e Windows.</span><span class="sxs-lookup"><span data-stu-id="add6e-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="add6e-145">Sì</span><span class="sxs-lookup"><span data-stu-id="add6e-145">Yes</span></span> |
| <span data-ttu-id="add6e-146">username</span><span class="sxs-lookup"><span data-stu-id="add6e-146">username</span></span> |<span data-ttu-id="add6e-147">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="add6e-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="add6e-148">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="add6e-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="add6e-149">password</span><span class="sxs-lookup"><span data-stu-id="add6e-149">password</span></span> |<span data-ttu-id="add6e-150">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="add6e-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="add6e-151">Sì (solo se si usa l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="add6e-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="add6e-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="add6e-152">authorizedCredential</span></span> |<span data-ttu-id="add6e-153">Se si usa OAuth, fare clic sul pulsante **Autorizza** nella procedura guidata di copia di Data Factory o nell'Editor e immettere le credenziali. Il valore di questa proprietà viene quindi generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="add6e-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="add6e-154">Sì (solo se si usa l'autenticazione OAuth)</span><span class="sxs-lookup"><span data-stu-id="add6e-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="add6e-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="add6e-155">gatewayName</span></span> |<span data-ttu-id="add6e-156">Nome del gateway che il servizio Data Factory deve usare per connettersi al servizio OData locale.</span><span class="sxs-lookup"><span data-stu-id="add6e-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="add6e-157">Specificare solo se si copiano dati da un'origine OData locale.</span><span class="sxs-lookup"><span data-stu-id="add6e-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="add6e-158">No</span><span class="sxs-lookup"><span data-stu-id="add6e-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="add6e-159">Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="add6e-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="add6e-160">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="add6e-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="add6e-161">Uso dell'autenticazione di Windows per accedere all'origine OData locale</span><span class="sxs-lookup"><span data-stu-id="add6e-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="add6e-162">Uso dell'autenticazione OAuth per accedere all'origine OData cloud</span><span class="sxs-lookup"><span data-stu-id="add6e-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="add6e-163">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="add6e-163">Dataset properties</span></span>
<span data-ttu-id="add6e-164">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="add6e-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="add6e-165">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="add6e-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="add6e-166">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="add6e-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="add6e-167">La sezione typeProperties per il set di dati di tipo **ODataResource** , che include il set di dati OData, presenta le proprietà seguenti</span><span class="sxs-lookup"><span data-stu-id="add6e-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="add6e-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="add6e-168">Property</span></span> | <span data-ttu-id="add6e-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="add6e-169">Description</span></span> | <span data-ttu-id="add6e-170">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="add6e-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="add6e-171">path</span><span class="sxs-lookup"><span data-stu-id="add6e-171">path</span></span> |<span data-ttu-id="add6e-172">Percorso della risorsa OData</span><span class="sxs-lookup"><span data-stu-id="add6e-172">Path to the OData resource</span></span> |<span data-ttu-id="add6e-173">No</span><span class="sxs-lookup"><span data-stu-id="add6e-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="add6e-174">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="add6e-174">Copy activity properties</span></span>
<span data-ttu-id="add6e-175">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="add6e-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="add6e-176">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="add6e-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="add6e-177">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="add6e-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="add6e-178">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="add6e-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="add6e-179">Se l'origine è di tipo **RelationalSource** (che comprende OData), nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="add6e-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="add6e-180">Proprietà</span><span class="sxs-lookup"><span data-stu-id="add6e-180">Property</span></span> | <span data-ttu-id="add6e-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="add6e-181">Description</span></span> | <span data-ttu-id="add6e-182">Esempio</span><span class="sxs-lookup"><span data-stu-id="add6e-182">Example</span></span> | <span data-ttu-id="add6e-183">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="add6e-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="add6e-184">query</span><span class="sxs-lookup"><span data-stu-id="add6e-184">query</span></span> |<span data-ttu-id="add6e-185">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="add6e-185">Use the custom query to read data.</span></span> |<span data-ttu-id="add6e-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="add6e-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="add6e-187">No</span><span class="sxs-lookup"><span data-stu-id="add6e-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="add6e-188">Mapping dei tipi per OData</span><span class="sxs-lookup"><span data-stu-id="add6e-188">Type Mapping for OData</span></span>
<span data-ttu-id="add6e-189">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipo automatiche dai tipi di origine ai tipi di sink con l'approccio in due passaggi seguente:</span><span class="sxs-lookup"><span data-stu-id="add6e-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="add6e-190">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="add6e-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="add6e-191">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="add6e-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="add6e-192">Quando si spostano dati da OData, vengono usati i mapping seguenti tra i tipi OData e i tipi .NET.</span><span class="sxs-lookup"><span data-stu-id="add6e-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="add6e-193">Tipo di dati OData</span><span class="sxs-lookup"><span data-stu-id="add6e-193">OData Data Type</span></span> | <span data-ttu-id="add6e-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="add6e-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="add6e-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="add6e-195">Edm.Binary</span></span> |<span data-ttu-id="add6e-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="add6e-196">Byte[]</span></span> |
| <span data-ttu-id="add6e-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="add6e-197">Edm.Boolean</span></span> |<span data-ttu-id="add6e-198">Booleano</span><span class="sxs-lookup"><span data-stu-id="add6e-198">Bool</span></span> |
| <span data-ttu-id="add6e-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="add6e-199">Edm.Byte</span></span> |<span data-ttu-id="add6e-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="add6e-200">Byte[]</span></span> |
| <span data-ttu-id="add6e-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="add6e-201">Edm.DateTime</span></span> |<span data-ttu-id="add6e-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="add6e-202">DateTime</span></span> |
| <span data-ttu-id="add6e-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="add6e-203">Edm.Decimal</span></span> |<span data-ttu-id="add6e-204">Decimale</span><span class="sxs-lookup"><span data-stu-id="add6e-204">Decimal</span></span> |
| <span data-ttu-id="add6e-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="add6e-205">Edm.Double</span></span> |<span data-ttu-id="add6e-206">Double</span><span class="sxs-lookup"><span data-stu-id="add6e-206">Double</span></span> |
| <span data-ttu-id="add6e-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="add6e-207">Edm.Single</span></span> |<span data-ttu-id="add6e-208">Single</span><span class="sxs-lookup"><span data-stu-id="add6e-208">Single</span></span> |
| <span data-ttu-id="add6e-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="add6e-209">Edm.Guid</span></span> |<span data-ttu-id="add6e-210">Guid</span><span class="sxs-lookup"><span data-stu-id="add6e-210">Guid</span></span> |
| <span data-ttu-id="add6e-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="add6e-211">Edm.Int16</span></span> |<span data-ttu-id="add6e-212">Int16</span><span class="sxs-lookup"><span data-stu-id="add6e-212">Int16</span></span> |
| <span data-ttu-id="add6e-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="add6e-213">Edm.Int32</span></span> |<span data-ttu-id="add6e-214">Int32</span><span class="sxs-lookup"><span data-stu-id="add6e-214">Int32</span></span> |
| <span data-ttu-id="add6e-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="add6e-215">Edm.Int64</span></span> |<span data-ttu-id="add6e-216">Int64</span><span class="sxs-lookup"><span data-stu-id="add6e-216">Int64</span></span> |
| <span data-ttu-id="add6e-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="add6e-217">Edm.SByte</span></span> |<span data-ttu-id="add6e-218">Int16</span><span class="sxs-lookup"><span data-stu-id="add6e-218">Int16</span></span> |
| <span data-ttu-id="add6e-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="add6e-219">Edm.String</span></span> |<span data-ttu-id="add6e-220">String</span><span class="sxs-lookup"><span data-stu-id="add6e-220">String</span></span> |
| <span data-ttu-id="add6e-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="add6e-221">Edm.Time</span></span> |<span data-ttu-id="add6e-222">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="add6e-222">TimeSpan</span></span> |
| <span data-ttu-id="add6e-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="add6e-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="add6e-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="add6e-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="add6e-225">Tipi di dati OData complessi. Gli oggetti, ad esempio, non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="add6e-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="add6e-226">Esempio JSON: Copiare dati da un'origine OData al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="add6e-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="add6e-227">Questo esempio fornisce le definizioni JSON di esempio da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="add6e-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="add6e-228">Illustrano come copiare dati da un'origine OData in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="add6e-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="add6e-229">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="add6e-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="add6e-230">L'esempio include le entità della data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="add6e-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="add6e-231">Un servizio collegato di tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="add6e-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="add6e-232">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="add6e-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="add6e-233">Un [set di dati](data-factory-create-datasets.md) di input di tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="add6e-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="add6e-234">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="add6e-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="add6e-235">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="add6e-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="add6e-236">L'esempio copia i dati dall'esecuzione di query su un'origine OData a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="add6e-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="add6e-237">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="add6e-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="add6e-238">**Servizio collegato OData:** questo esempio usa l'autenticazione anonima.</span><span class="sxs-lookup"><span data-stu-id="add6e-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="add6e-239">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato OData](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="add6e-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="add6e-240">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="add6e-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="add6e-241">**Set di dati di input OData:**</span><span class="sxs-lookup"><span data-stu-id="add6e-241">**OData input dataset:**</span></span>

<span data-ttu-id="add6e-242">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="add6e-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="add6e-243">La specifica di **path** nella definizione del set di dati è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="add6e-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="add6e-244">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="add6e-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="add6e-245">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="add6e-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="add6e-246">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="add6e-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="add6e-247">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="add6e-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="add6e-248">**Attività di copia in una pipeline con un'origine OData e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="add6e-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="add6e-249">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="add6e-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="add6e-250">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="add6e-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="add6e-251">La query SQL specificata per la proprietà **query** seleziona i dati più recenti dall'origine OData.</span><span class="sxs-lookup"><span data-stu-id="add6e-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

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

<span data-ttu-id="add6e-252">La specifica di **query** nella definizione della pipeline è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="add6e-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="add6e-253">L' **URL** è che il servizio Data Factory usa per recuperare i dati è il seguente: URL specificato nel servizio collegato (obbligatorio) + percorso specificato nel set di dati (facoltativo) + query nella pipeline (facoltativa).</span><span class="sxs-lookup"><span data-stu-id="add6e-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="add6e-254">Mapping dei tipi per OData</span><span class="sxs-lookup"><span data-stu-id="add6e-254">Type mapping for OData</span></span>
<span data-ttu-id="add6e-255">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="add6e-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="add6e-256">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="add6e-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="add6e-257">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="add6e-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="add6e-258">Quando i dati vengono spostati da archivi OData, i tipi di dati OData vengono mappati ai tipi .NET.</span><span class="sxs-lookup"><span data-stu-id="add6e-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="add6e-259">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="add6e-259">Map source to sink columns</span></span>
<span data-ttu-id="add6e-260">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="add6e-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="add6e-261">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="add6e-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="add6e-262">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="add6e-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="add6e-263">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="add6e-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="add6e-264">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="add6e-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="add6e-265">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="add6e-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="add6e-266">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="add6e-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="add6e-267">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="add6e-267">Performance and Tuning</span></span>
<span data-ttu-id="add6e-268">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="add6e-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
