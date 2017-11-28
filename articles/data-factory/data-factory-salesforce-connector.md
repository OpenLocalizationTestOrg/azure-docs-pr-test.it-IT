---
title: dati aaaMove da Salesforce utilizzando Data Factory | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da Salesforce utilizzando Data Factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="1922b-103">Spostare dati da Salesforce usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1922b-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="1922b-104">In questo articolo descrive come è possibile utilizzare l'attività di copia in un Azure factory toocopy dati dall'archivio di dati Salesforce tooany elencato nella colonna Sink hello hello [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="1922b-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1922b-105">In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia e combinazioni di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="1922b-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="1922b-106">Data Factory di Azure attualmente supporta solo lo spostamento dei dati da Salesforce troppo[supportati archivi dati sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ma non supporta lo spostamento dei dati da altri tooSalesforce di archivi dati.</span><span class="sxs-lookup"><span data-stu-id="1922b-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="1922b-107">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="1922b-107">Supported versions</span></span>
<span data-ttu-id="1922b-108">Questo connettore supporta hello seguenti edizioni di Salesforce: edizione illimitato, Professional Edition, Enterprise Edition o Developer Edition.</span><span class="sxs-lookup"><span data-stu-id="1922b-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="1922b-109">Supporta anche la copia dall'ambiente di produzione, dalla sandbox e dal dominio personalizzato di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="1922b-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1922b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1922b-110">Prerequisites</span></span>
* <span data-ttu-id="1922b-111">È necessario abilitare l'autorizzazione API.</span><span class="sxs-lookup"><span data-stu-id="1922b-111">API permission must be enabled.</span></span> <span data-ttu-id="1922b-112">Vedere [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="1922b-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="1922b-113">toocopy dati da archivi dati di Salesforce tooon locali, è necessario disporre almeno Data Management Gateway 2.0 installato nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="1922b-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="1922b-114">Limiti delle richieste Salesforce</span><span class="sxs-lookup"><span data-stu-id="1922b-114">Salesforce request limits</span></span>
<span data-ttu-id="1922b-115">Salesforce presenta limiti per le richieste API totali e per le richieste API simultanee.</span><span class="sxs-lookup"><span data-stu-id="1922b-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="1922b-116">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="1922b-116">Note hello following points:</span></span>

- <span data-ttu-id="1922b-117">Se il numero di hello di richieste simultanee supera il limite di hello, si verifica una limitazione e verranno visualizzati errori casuali.</span><span class="sxs-lookup"><span data-stu-id="1922b-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="1922b-118">Se il numero totale di hello di richieste supera il limite di hello, hello account Salesforce verrà bloccato per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="1922b-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="1922b-119">È inoltre possibile ricevere l'errore "REQUEST_LIMIT_EXCEEDED" hello in entrambi gli scenari.</span><span class="sxs-lookup"><span data-stu-id="1922b-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="1922b-120">Nella sezione hello "API di limiti richiesta" hello [Salesforce Developer limiti](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) articolo per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="1922b-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1922b-121">introduttiva</span><span class="sxs-lookup"><span data-stu-id="1922b-121">Getting started</span></span>
<span data-ttu-id="1922b-122">È possibile creare una pipeline con l'attività di copia che sposta i dati da Salesforce usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="1922b-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="1922b-123">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="1922b-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="1922b-124">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="1922b-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="1922b-125">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="1922b-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1922b-126">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="1922b-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1922b-127">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="1922b-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="1922b-128">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="1922b-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="1922b-129">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="1922b-130">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="1922b-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1922b-131">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="1922b-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="1922b-132">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1922b-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="1922b-133">Per un esempio con le definizioni di JSON per le entità Data Factory toocopy utilizzati dati di Salesforce, vedere [esempio JSON: copiare i dati da Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1922b-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1922b-134">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooSalesforce:</span><span class="sxs-lookup"><span data-stu-id="1922b-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="1922b-135">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="1922b-135">Linked service properties</span></span>
<span data-ttu-id="1922b-136">Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON sono toohello specifico del servizio collegato di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="1922b-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="1922b-137">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1922b-137">Property</span></span> | <span data-ttu-id="1922b-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1922b-138">Description</span></span> | <span data-ttu-id="1922b-139">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1922b-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1922b-140">type</span><span class="sxs-lookup"><span data-stu-id="1922b-140">type</span></span> |<span data-ttu-id="1922b-141">proprietà di tipo Hello deve essere impostata su: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="1922b-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="1922b-142">Sì</span><span class="sxs-lookup"><span data-stu-id="1922b-142">Yes</span></span> |
| <span data-ttu-id="1922b-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="1922b-143">environmentUrl</span></span> | <span data-ttu-id="1922b-144">Specificare l'istanza di URL di Salesforce hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="1922b-145">- Il valore predefinito è "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="1922b-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="1922b-146">-toocopy dati dalla sandbox, specificare "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="1922b-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="1922b-147">-toocopy dati da un dominio personalizzato, specificare, ad esempio, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="1922b-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="1922b-148">No</span><span class="sxs-lookup"><span data-stu-id="1922b-148">No</span></span> |
| <span data-ttu-id="1922b-149">username</span><span class="sxs-lookup"><span data-stu-id="1922b-149">username</span></span> |<span data-ttu-id="1922b-150">Specificare un nome utente per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="1922b-151">Sì</span><span class="sxs-lookup"><span data-stu-id="1922b-151">Yes</span></span> |
| <span data-ttu-id="1922b-152">password</span><span class="sxs-lookup"><span data-stu-id="1922b-152">password</span></span> |<span data-ttu-id="1922b-153">Specificare una password per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="1922b-154">Sì</span><span class="sxs-lookup"><span data-stu-id="1922b-154">Yes</span></span> |
| <span data-ttu-id="1922b-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="1922b-155">securityToken</span></span> |<span data-ttu-id="1922b-156">Specificare un token di sicurezza per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="1922b-157">Vedere [ottenere token di sicurezza](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) per istruzioni su come un token di sicurezza tooreset/get.</span><span class="sxs-lookup"><span data-stu-id="1922b-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="1922b-158">in generale, vedere toolearn sui token di sicurezza [API di protezione e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="1922b-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="1922b-159">Sì</span><span class="sxs-lookup"><span data-stu-id="1922b-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="1922b-160">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="1922b-160">Dataset properties</span></span>
<span data-ttu-id="1922b-161">Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="1922b-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1922b-162">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="1922b-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="1922b-163">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="1922b-164">sezione Hello typeProperties per un set di dati di tipo hello **RelationalTable** è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="1922b-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="1922b-165">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1922b-165">Property</span></span> | <span data-ttu-id="1922b-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1922b-166">Description</span></span> | <span data-ttu-id="1922b-167">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1922b-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1922b-168">tableName</span><span class="sxs-lookup"><span data-stu-id="1922b-168">tableName</span></span> |<span data-ttu-id="1922b-169">Nome della tabella hello in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="1922b-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="1922b-170">No, se è specificata una **query** di **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="1922b-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1922b-171">parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1922b-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="1922b-173">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="1922b-173">Copy activity properties</span></span>
<span data-ttu-id="1922b-174">Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di attività, vedere hello [creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="1922b-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1922b-175">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e diversi criteri.</span><span class="sxs-lookup"><span data-stu-id="1922b-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="1922b-176">sono disponibili nella proprietà Hello hello sezione typeProperties di attività hello hello invece, variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="1922b-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="1922b-177">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="1922b-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="1922b-178">Nell'attività di copia, se l'origine hello è di tipo hello **RelationalSource** (che include Salesforce), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="1922b-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1922b-179">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1922b-179">Property</span></span> | <span data-ttu-id="1922b-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1922b-180">Description</span></span> | <span data-ttu-id="1922b-181">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="1922b-181">Allowed values</span></span> | <span data-ttu-id="1922b-182">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1922b-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1922b-183">query</span><span class="sxs-lookup"><span data-stu-id="1922b-183">query</span></span> |<span data-ttu-id="1922b-184">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1922b-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="1922b-185">Query SQL-92 o query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="1922b-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="1922b-186">Ad esempio: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="1922b-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="1922b-187">No (se hello **tableName** di hello **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="1922b-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1922b-188">parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1922b-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="1922b-190">Suggerimenti di query</span><span class="sxs-lookup"><span data-stu-id="1922b-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="1922b-191">Recupero di dati tramite la clausola where nella colonna DateTime</span><span class="sxs-lookup"><span data-stu-id="1922b-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="1922b-192">Specificare quando hello SOQL o SQL query, pagamento attenzione toohello differenza formato DateTime.</span><span class="sxs-lookup"><span data-stu-id="1922b-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="1922b-193">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1922b-193">For example:</span></span>

* <span data-ttu-id="1922b-194">**Esempio SOQL**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="1922b-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="1922b-195">**Esempio SQL**:</span><span class="sxs-lookup"><span data-stu-id="1922b-195">**SQL sample**:</span></span>
    * <span data-ttu-id="1922b-196">**Tramite Copia guidata toospecify hello query:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="1922b-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="1922b-197">**Mediante la modifica di query hello toospecify (carattere di escape correttamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="1922b-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="1922b-198">Recupero di dati dal report di Salesforce</span><span class="sxs-lookup"><span data-stu-id="1922b-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="1922b-199">È possibile recuperare i dati dai report di Salesforce specificando una query come `{call "<report name>"}`, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="1922b-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="1922b-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="1922b-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="1922b-201">Recupero dei record eliminati dal Cestino di Salesforce</span><span class="sxs-lookup"><span data-stu-id="1922b-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="1922b-202">record di tooquery hello soft eliminato dal Cestino di Salesforce, è possibile specificare **"IsDeleted = 1"** nella query.</span><span class="sxs-lookup"><span data-stu-id="1922b-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="1922b-203">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="1922b-203">For example,</span></span>

* <span data-ttu-id="1922b-204">specificare tooquery solo i record eliminato hello, "selezionare * da MyTable__c **dove IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="1922b-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="1922b-205">tooquery tutti hello record inclusi hello esistente e hello eliminato, specificare "Seleziona * da MyTable__c **dove IsDeleted = 0 o IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="1922b-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="1922b-206">Esempio JSON: copiare i dati da Salesforce tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="1922b-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="1922b-207">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1922b-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1922b-208">Vengono visualizzate come dati toocopy da Salesforce tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="1922b-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="1922b-209">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1922b-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="1922b-210">Di seguito sono gli elementi Data Factory di hello che è necessario uno scenario di hello tooimplement toocreate.</span><span class="sxs-lookup"><span data-stu-id="1922b-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="1922b-211">Hello che seguono l'elenco di hello che forniscono informazioni dettagliate su questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="1922b-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="1922b-212">Un servizio collegato di tipo hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1922b-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="1922b-213">Un servizio collegato di tipo hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="1922b-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="1922b-214">Un input [dataset](data-factory-create-datasets.md) di tipo hello [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="1922b-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="1922b-215">Un output [dataset](data-factory-create-datasets.md) di tipo hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="1922b-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="1922b-216">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="1922b-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="1922b-217">**Servizio collegato Salesforce**</span><span class="sxs-lookup"><span data-stu-id="1922b-217">**Salesforce linked service**</span></span>

<span data-ttu-id="1922b-218">Questo esempio viene utilizzato hello **Salesforce** servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="1922b-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="1922b-219">Vedere hello [servizio collegato di Salesforce](#linked-service-properties) sezione per le proprietà di hello supportati da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="1922b-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="1922b-220">Vedere [ottenere token di sicurezza](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) per istruzioni su come tooreset/get hello token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1922b-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="1922b-221">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="1922b-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="1922b-222">**Set di dati di input Salesforce**</span><span class="sxs-lookup"><span data-stu-id="1922b-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

<span data-ttu-id="1922b-223">Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="1922b-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1922b-224">parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1922b-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="1922b-226">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="1922b-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="1922b-227">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="1922b-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1922b-228">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="1922b-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="1922b-229">pipeline Hello contiene le attività di copia, che viene configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="1922b-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="1922b-230">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource**, hello e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1922b-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="1922b-231">Vedere [le proprietà del tipo RelationalSource](#copy-activity-properties) per elenco hello delle proprietà supportate da hello RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="1922b-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]
    }
}
```
> [!IMPORTANT]
> <span data-ttu-id="1922b-232">parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1922b-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="1922b-234">Mapping dei tipi per Salesforce</span><span class="sxs-lookup"><span data-stu-id="1922b-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="1922b-235">Tipo Salesforce</span><span class="sxs-lookup"><span data-stu-id="1922b-235">Salesforce type</span></span> | <span data-ttu-id="1922b-236">Tipo basato su .NET</span><span class="sxs-lookup"><span data-stu-id="1922b-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="1922b-237">Numero automatico</span><span class="sxs-lookup"><span data-stu-id="1922b-237">Auto Number</span></span> |<span data-ttu-id="1922b-238">String</span><span class="sxs-lookup"><span data-stu-id="1922b-238">String</span></span> |
| <span data-ttu-id="1922b-239">Casella di controllo</span><span class="sxs-lookup"><span data-stu-id="1922b-239">Checkbox</span></span> |<span data-ttu-id="1922b-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="1922b-240">Boolean</span></span> |
| <span data-ttu-id="1922b-241">Valuta</span><span class="sxs-lookup"><span data-stu-id="1922b-241">Currency</span></span> |<span data-ttu-id="1922b-242">Double</span><span class="sxs-lookup"><span data-stu-id="1922b-242">Double</span></span> |
| <span data-ttu-id="1922b-243">Data</span><span class="sxs-lookup"><span data-stu-id="1922b-243">Date</span></span> |<span data-ttu-id="1922b-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="1922b-244">DateTime</span></span> |
| <span data-ttu-id="1922b-245">Data/ora</span><span class="sxs-lookup"><span data-stu-id="1922b-245">Date/Time</span></span> |<span data-ttu-id="1922b-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="1922b-246">DateTime</span></span> |
| <span data-ttu-id="1922b-247">Email</span><span class="sxs-lookup"><span data-stu-id="1922b-247">Email</span></span> |<span data-ttu-id="1922b-248">String</span><span class="sxs-lookup"><span data-stu-id="1922b-248">String</span></span> |
| <span data-ttu-id="1922b-249">ID</span><span class="sxs-lookup"><span data-stu-id="1922b-249">Id</span></span> |<span data-ttu-id="1922b-250">String</span><span class="sxs-lookup"><span data-stu-id="1922b-250">String</span></span> |
| <span data-ttu-id="1922b-251">Relazione di ricerca</span><span class="sxs-lookup"><span data-stu-id="1922b-251">Lookup Relationship</span></span> |<span data-ttu-id="1922b-252">String</span><span class="sxs-lookup"><span data-stu-id="1922b-252">String</span></span> |
| <span data-ttu-id="1922b-253">Elenco a discesa seleziona multipla</span><span class="sxs-lookup"><span data-stu-id="1922b-253">Multi-Select Picklist</span></span> |<span data-ttu-id="1922b-254">String</span><span class="sxs-lookup"><span data-stu-id="1922b-254">String</span></span> |
| <span data-ttu-id="1922b-255">Number</span><span class="sxs-lookup"><span data-stu-id="1922b-255">Number</span></span> |<span data-ttu-id="1922b-256">Double</span><span class="sxs-lookup"><span data-stu-id="1922b-256">Double</span></span> |
| <span data-ttu-id="1922b-257">Percentuale</span><span class="sxs-lookup"><span data-stu-id="1922b-257">Percent</span></span> |<span data-ttu-id="1922b-258">Double</span><span class="sxs-lookup"><span data-stu-id="1922b-258">Double</span></span> |
| <span data-ttu-id="1922b-259">Telefono</span><span class="sxs-lookup"><span data-stu-id="1922b-259">Phone</span></span> |<span data-ttu-id="1922b-260">String</span><span class="sxs-lookup"><span data-stu-id="1922b-260">String</span></span> |
| <span data-ttu-id="1922b-261">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="1922b-261">Picklist</span></span> |<span data-ttu-id="1922b-262">String</span><span class="sxs-lookup"><span data-stu-id="1922b-262">String</span></span> |
| <span data-ttu-id="1922b-263">Text</span><span class="sxs-lookup"><span data-stu-id="1922b-263">Text</span></span> |<span data-ttu-id="1922b-264">String</span><span class="sxs-lookup"><span data-stu-id="1922b-264">String</span></span> |
| <span data-ttu-id="1922b-265">Area di testo</span><span class="sxs-lookup"><span data-stu-id="1922b-265">Text Area</span></span> |<span data-ttu-id="1922b-266">String</span><span class="sxs-lookup"><span data-stu-id="1922b-266">String</span></span> |
| <span data-ttu-id="1922b-267">Area di testo (Long)</span><span class="sxs-lookup"><span data-stu-id="1922b-267">Text Area (Long)</span></span> |<span data-ttu-id="1922b-268">String</span><span class="sxs-lookup"><span data-stu-id="1922b-268">String</span></span> |
| <span data-ttu-id="1922b-269">Area di testo (Rich)</span><span class="sxs-lookup"><span data-stu-id="1922b-269">Text Area (Rich)</span></span> |<span data-ttu-id="1922b-270">String</span><span class="sxs-lookup"><span data-stu-id="1922b-270">String</span></span> |
| <span data-ttu-id="1922b-271">Testo (Crittografato)</span><span class="sxs-lookup"><span data-stu-id="1922b-271">Text (Encrypted)</span></span> |<span data-ttu-id="1922b-272">String</span><span class="sxs-lookup"><span data-stu-id="1922b-272">String</span></span> |
| <span data-ttu-id="1922b-273">URL</span><span class="sxs-lookup"><span data-stu-id="1922b-273">URL</span></span> |<span data-ttu-id="1922b-274">String</span><span class="sxs-lookup"><span data-stu-id="1922b-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="1922b-275">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1922b-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="1922b-276">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="1922b-276">Performance and tuning</span></span>
<span data-ttu-id="1922b-277">Vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="1922b-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
