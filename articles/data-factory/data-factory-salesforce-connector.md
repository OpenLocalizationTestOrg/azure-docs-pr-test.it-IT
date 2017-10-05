---
title: Spostare i dati da Salesforce usando Data Factory | Documentazione Microsoft
description: Informazioni su come spostare dati da Salesforce usando Azure Data Factory.
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
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="24f35-103">Spostare dati da Salesforce usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="24f35-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="24f35-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per copiare dati da Salesforce in qualsiasi archivio dati elencato nella colonna Sink della tabella relativa a [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="24f35-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="24f35-105">Questo articolo si basa sull'articolo [Spostamento di dati e attività di copia](data-factory-data-movement-activities.md) , che offre una panoramica generale dello spostamento dei dati con attività di copia e delle combinazioni di archivi dati supportati.</span><span class="sxs-lookup"><span data-stu-id="24f35-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="24f35-106">Attualmente Azure Data Factory supporta solo lo spostamento di dati da Salesforce verso gli [archivi dati sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ma non supporta lo spostamento di dati da altri archivi dati a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="24f35-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="24f35-107">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="24f35-107">Supported versions</span></span>
<span data-ttu-id="24f35-108">Questo connettore supporta le edizioni di Salesforce seguenti: Developer Edition, Professional Edition, Enterprise Edition o Unlimited Edition.</span><span class="sxs-lookup"><span data-stu-id="24f35-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="24f35-109">Supporta anche la copia dall'ambiente di produzione, dalla sandbox e dal dominio personalizzato di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="24f35-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24f35-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="24f35-110">Prerequisites</span></span>
* <span data-ttu-id="24f35-111">È necessario abilitare l'autorizzazione API.</span><span class="sxs-lookup"><span data-stu-id="24f35-111">API permission must be enabled.</span></span> <span data-ttu-id="24f35-112">Vedere [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="24f35-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="24f35-113">Per copiare dati da Salesforce in archivi dati locali, è necessario che nell'ambiente locale sia installato almeno Gateway di gestione dati 2.0.</span><span class="sxs-lookup"><span data-stu-id="24f35-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="24f35-114">Limiti delle richieste Salesforce</span><span class="sxs-lookup"><span data-stu-id="24f35-114">Salesforce request limits</span></span>
<span data-ttu-id="24f35-115">Salesforce presenta limiti per le richieste API totali e per le richieste API simultanee.</span><span class="sxs-lookup"><span data-stu-id="24f35-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="24f35-116">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="24f35-116">Note the following points:</span></span>

- <span data-ttu-id="24f35-117">Se il numero di richieste simultanee supera il limite, si verifica una limitazione e vengono visualizzati errori casuali.</span><span class="sxs-lookup"><span data-stu-id="24f35-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="24f35-118">Se il numero totale di richieste supera il limite, l'account di Salesforce verrà bloccato per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="24f35-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="24f35-119">In entrambi gli scenari è anche possibile che venga visualizzato l'errore "REQUEST_LIMIT_EXCEEDED" ("LIMITE_RICHIESTE_SUPERATO").</span><span class="sxs-lookup"><span data-stu-id="24f35-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="24f35-120">Per i dettagli, vedere la sezione API Request Limits (Limiti delle richieste API) nell'articolo [Salesforce API Request Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) (Limiti delle richieste API di Salesforce).</span><span class="sxs-lookup"><span data-stu-id="24f35-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="24f35-121">Introduzione</span><span class="sxs-lookup"><span data-stu-id="24f35-121">Getting started</span></span>
<span data-ttu-id="24f35-122">È possibile creare una pipeline con l'attività di copia che sposta i dati da Salesforce usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="24f35-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="24f35-123">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="24f35-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="24f35-124">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="24f35-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="24f35-125">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="24f35-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="24f35-126">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="24f35-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="24f35-127">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="24f35-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="24f35-128">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="24f35-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="24f35-129">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="24f35-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="24f35-130">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="24f35-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="24f35-131">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="24f35-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="24f35-132">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="24f35-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="24f35-133">Per un esempio con le definizioni JSON per le entità di Data Factory usate per copiare dati da Salesforce, vedere la sezione [Esempio JSON: Copiare dati da Salesforce a BLOB di Azure](#json-example-copy-data-from-salesforce-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="24f35-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="24f35-134">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di Salesforce:</span><span class="sxs-lookup"><span data-stu-id="24f35-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="24f35-135">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="24f35-135">Linked service properties</span></span>
<span data-ttu-id="24f35-136">La tabella seguente include le descrizioni degli elementi JSON specifici del servizio collegato Salesforce.</span><span class="sxs-lookup"><span data-stu-id="24f35-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="24f35-137">Proprietà</span><span class="sxs-lookup"><span data-stu-id="24f35-137">Property</span></span> | <span data-ttu-id="24f35-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="24f35-138">Description</span></span> | <span data-ttu-id="24f35-139">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="24f35-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24f35-140">type</span><span class="sxs-lookup"><span data-stu-id="24f35-140">type</span></span> |<span data-ttu-id="24f35-141">La proprietà type deve essere impostata su **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="24f35-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="24f35-142">Sì</span><span class="sxs-lookup"><span data-stu-id="24f35-142">Yes</span></span> |
| <span data-ttu-id="24f35-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="24f35-143">environmentUrl</span></span> | <span data-ttu-id="24f35-144">Specificare l'URL dell'istanza di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="24f35-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="24f35-145">- Il valore predefinito è "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="24f35-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="24f35-146">- Per copiare i dati dalla sandbox, specificare "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="24f35-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="24f35-147">- Per copiare i dati dal dominio personalizzato, specificare ad esempio "https://[dominio].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="24f35-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="24f35-148">No</span><span class="sxs-lookup"><span data-stu-id="24f35-148">No</span></span> |
| <span data-ttu-id="24f35-149">username</span><span class="sxs-lookup"><span data-stu-id="24f35-149">username</span></span> |<span data-ttu-id="24f35-150">Specificare un nome utente per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="24f35-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="24f35-151">Sì</span><span class="sxs-lookup"><span data-stu-id="24f35-151">Yes</span></span> |
| <span data-ttu-id="24f35-152">password</span><span class="sxs-lookup"><span data-stu-id="24f35-152">password</span></span> |<span data-ttu-id="24f35-153">Specificare la password per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="24f35-153">Specify a password for the user account.</span></span> |<span data-ttu-id="24f35-154">Sì</span><span class="sxs-lookup"><span data-stu-id="24f35-154">Yes</span></span> |
| <span data-ttu-id="24f35-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="24f35-155">securityToken</span></span> |<span data-ttu-id="24f35-156">Specificare un token di sicurezza per l'account utente.</span><span class="sxs-lookup"><span data-stu-id="24f35-156">Specify a security token for the user account.</span></span> <span data-ttu-id="24f35-157">Per istruzioni su come ottenere o reimpostare un token di sicurezza, vedere [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Ottenere un token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="24f35-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="24f35-158">Per informazioni generali sui token di sicurezza, vedere [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Sicurezza e API).</span><span class="sxs-lookup"><span data-stu-id="24f35-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="24f35-159">Sì</span><span class="sxs-lookup"><span data-stu-id="24f35-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="24f35-160">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="24f35-160">Dataset properties</span></span>
<span data-ttu-id="24f35-161">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo [Set di dati in Azure Data Factory](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="24f35-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="24f35-162">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="24f35-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="24f35-163">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="24f35-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="24f35-164">La sezione typeProperties per un set di dati di tipo **RelationalTable** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="24f35-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="24f35-165">Proprietà</span><span class="sxs-lookup"><span data-stu-id="24f35-165">Property</span></span> | <span data-ttu-id="24f35-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="24f35-166">Description</span></span> | <span data-ttu-id="24f35-167">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="24f35-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24f35-168">tableName</span><span class="sxs-lookup"><span data-stu-id="24f35-168">tableName</span></span> |<span data-ttu-id="24f35-169">Nome della tabella in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="24f35-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="24f35-170">No, se è specificata una **query** di **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="24f35-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="24f35-171">La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="24f35-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="24f35-173">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="24f35-173">Copy activity properties</span></span>
<span data-ttu-id="24f35-174">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo relativo alla [creazione di pipeline](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="24f35-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="24f35-175">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e diversi criteri.</span><span class="sxs-lookup"><span data-stu-id="24f35-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="24f35-176">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="24f35-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="24f35-177">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="24f35-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="24f35-178">Nell'attività di copia, quando l'origine è di tipo **RelationalSource** (che include Salesforce), nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="24f35-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="24f35-179">Proprietà</span><span class="sxs-lookup"><span data-stu-id="24f35-179">Property</span></span> | <span data-ttu-id="24f35-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="24f35-180">Description</span></span> | <span data-ttu-id="24f35-181">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="24f35-181">Allowed values</span></span> | <span data-ttu-id="24f35-182">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="24f35-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="24f35-183">query</span><span class="sxs-lookup"><span data-stu-id="24f35-183">query</span></span> |<span data-ttu-id="24f35-184">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="24f35-184">Use the custom query to read data.</span></span> |<span data-ttu-id="24f35-185">Query SQL-92 o query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="24f35-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="24f35-186">Ad esempio: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="24f35-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="24f35-187">No, se è specificato **tableName** per il **set di dati**</span><span class="sxs-lookup"><span data-stu-id="24f35-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="24f35-188">La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="24f35-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="24f35-190">Suggerimenti di query</span><span class="sxs-lookup"><span data-stu-id="24f35-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="24f35-191">Recupero di dati tramite la clausola where nella colonna DateTime</span><span class="sxs-lookup"><span data-stu-id="24f35-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="24f35-192">Quando si specifica la query SQL o SOQL, prestare attenzione alla differenza di formato di DateTime.</span><span class="sxs-lookup"><span data-stu-id="24f35-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="24f35-193">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="24f35-193">For example:</span></span>

* <span data-ttu-id="24f35-194">**Esempio SOQL**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="24f35-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="24f35-195">**Esempio SQL**:</span><span class="sxs-lookup"><span data-stu-id="24f35-195">**SQL sample**:</span></span>
    * <span data-ttu-id="24f35-196">**Uso della procedura di copia guidata per specificare la query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="24f35-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="24f35-197">**Uso della modifica JSON per specificare la query (usare correttamente il carattere di escape):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="24f35-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="24f35-198">Recupero di dati dal report di Salesforce</span><span class="sxs-lookup"><span data-stu-id="24f35-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="24f35-199">È possibile recuperare i dati dai report di Salesforce specificando una query come `{call "<report name>"}`, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="24f35-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="24f35-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="24f35-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="24f35-201">Recupero dei record eliminati dal Cestino di Salesforce</span><span class="sxs-lookup"><span data-stu-id="24f35-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="24f35-202">Per eseguire una query sui record eliminati temporaneamente dal Cestino di Salesforce, è possibile specificare **"IsDeleted = 1"** nella query.</span><span class="sxs-lookup"><span data-stu-id="24f35-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="24f35-203">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="24f35-203">For example,</span></span>

* <span data-ttu-id="24f35-204">Per eseguire una query solo sui record eliminati, specificare MyTable__c **where IsDeleted= 1**"</span><span class="sxs-lookup"><span data-stu-id="24f35-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="24f35-205">Per eseguire query su tutti i record inclusi quelli esistenti ed eliminati, specificare "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="24f35-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="24f35-206">Esempio JSON: Copiare dati da Salesforce a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="24f35-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="24f35-207">L'esempio seguente fornisce le definizioni JSON si esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="24f35-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="24f35-208">Illustrano come copiare dati da Salesforce in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="24f35-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="24f35-209">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="24f35-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="24f35-210">Ecco gli elementi di Data Factory che è necessario creare per implementare lo scenario.</span><span class="sxs-lookup"><span data-stu-id="24f35-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="24f35-211">Le sezioni che seguono l'elenco forniscono informazioni dettagliate su questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="24f35-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="24f35-212">Un servizio collegato di tipo [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="24f35-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="24f35-213">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="24f35-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="24f35-214">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="24f35-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="24f35-215">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="24f35-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="24f35-216">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="24f35-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="24f35-217">**Servizio collegato Salesforce**</span><span class="sxs-lookup"><span data-stu-id="24f35-217">**Salesforce linked service**</span></span>

<span data-ttu-id="24f35-218">Questo esempio usa il servizio collegato **Salesforce** .</span><span class="sxs-lookup"><span data-stu-id="24f35-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="24f35-219">Per informazioni sulle proprietà supportate da questo servizio collegato, vedere la sezione [Proprietà del servizio collegato Salesforce](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="24f35-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="24f35-220">Per istruzioni su come ottenere o reimpostare un token di sicurezza, vedere [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Ottenere un token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="24f35-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

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
<span data-ttu-id="24f35-221">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="24f35-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="24f35-222">**Set di dati di input Salesforce**</span><span class="sxs-lookup"><span data-stu-id="24f35-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="24f35-223">Impostando **external** su **true** si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="24f35-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24f35-224">La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="24f35-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="24f35-226">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="24f35-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="24f35-227">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="24f35-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="24f35-228">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="24f35-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="24f35-229">La pipeline contiene un'attività di copia configurata per l'uso dei set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="24f35-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="24f35-230">Nella definizione JSON della pipeline il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="24f35-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="24f35-231">Per l'elenco delle proprietà supportate da RelationalSource, vedere [Proprietà del tipo RelationalSource](#copy-activity-properties) .</span><span class="sxs-lookup"><span data-stu-id="24f35-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

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
            "description": "Copy from Salesforce to an Azure blob",
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
> <span data-ttu-id="24f35-232">La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="24f35-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="24f35-234">Mapping dei tipi per Salesforce</span><span class="sxs-lookup"><span data-stu-id="24f35-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="24f35-235">Tipo Salesforce</span><span class="sxs-lookup"><span data-stu-id="24f35-235">Salesforce type</span></span> | <span data-ttu-id="24f35-236">Tipo basato su .NET</span><span class="sxs-lookup"><span data-stu-id="24f35-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="24f35-237">Numero automatico</span><span class="sxs-lookup"><span data-stu-id="24f35-237">Auto Number</span></span> |<span data-ttu-id="24f35-238">String</span><span class="sxs-lookup"><span data-stu-id="24f35-238">String</span></span> |
| <span data-ttu-id="24f35-239">Casella di controllo</span><span class="sxs-lookup"><span data-stu-id="24f35-239">Checkbox</span></span> |<span data-ttu-id="24f35-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="24f35-240">Boolean</span></span> |
| <span data-ttu-id="24f35-241">Valuta</span><span class="sxs-lookup"><span data-stu-id="24f35-241">Currency</span></span> |<span data-ttu-id="24f35-242">Double</span><span class="sxs-lookup"><span data-stu-id="24f35-242">Double</span></span> |
| <span data-ttu-id="24f35-243">Data</span><span class="sxs-lookup"><span data-stu-id="24f35-243">Date</span></span> |<span data-ttu-id="24f35-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="24f35-244">DateTime</span></span> |
| <span data-ttu-id="24f35-245">Data/ora</span><span class="sxs-lookup"><span data-stu-id="24f35-245">Date/Time</span></span> |<span data-ttu-id="24f35-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="24f35-246">DateTime</span></span> |
| <span data-ttu-id="24f35-247">Email</span><span class="sxs-lookup"><span data-stu-id="24f35-247">Email</span></span> |<span data-ttu-id="24f35-248">String</span><span class="sxs-lookup"><span data-stu-id="24f35-248">String</span></span> |
| <span data-ttu-id="24f35-249">ID</span><span class="sxs-lookup"><span data-stu-id="24f35-249">Id</span></span> |<span data-ttu-id="24f35-250">String</span><span class="sxs-lookup"><span data-stu-id="24f35-250">String</span></span> |
| <span data-ttu-id="24f35-251">Relazione di ricerca</span><span class="sxs-lookup"><span data-stu-id="24f35-251">Lookup Relationship</span></span> |<span data-ttu-id="24f35-252">String</span><span class="sxs-lookup"><span data-stu-id="24f35-252">String</span></span> |
| <span data-ttu-id="24f35-253">Elenco a discesa seleziona multipla</span><span class="sxs-lookup"><span data-stu-id="24f35-253">Multi-Select Picklist</span></span> |<span data-ttu-id="24f35-254">String</span><span class="sxs-lookup"><span data-stu-id="24f35-254">String</span></span> |
| <span data-ttu-id="24f35-255">Number</span><span class="sxs-lookup"><span data-stu-id="24f35-255">Number</span></span> |<span data-ttu-id="24f35-256">Double</span><span class="sxs-lookup"><span data-stu-id="24f35-256">Double</span></span> |
| <span data-ttu-id="24f35-257">Percentuale</span><span class="sxs-lookup"><span data-stu-id="24f35-257">Percent</span></span> |<span data-ttu-id="24f35-258">Double</span><span class="sxs-lookup"><span data-stu-id="24f35-258">Double</span></span> |
| <span data-ttu-id="24f35-259">Telefono</span><span class="sxs-lookup"><span data-stu-id="24f35-259">Phone</span></span> |<span data-ttu-id="24f35-260">String</span><span class="sxs-lookup"><span data-stu-id="24f35-260">String</span></span> |
| <span data-ttu-id="24f35-261">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="24f35-261">Picklist</span></span> |<span data-ttu-id="24f35-262">String</span><span class="sxs-lookup"><span data-stu-id="24f35-262">String</span></span> |
| <span data-ttu-id="24f35-263">Text</span><span class="sxs-lookup"><span data-stu-id="24f35-263">Text</span></span> |<span data-ttu-id="24f35-264">String</span><span class="sxs-lookup"><span data-stu-id="24f35-264">String</span></span> |
| <span data-ttu-id="24f35-265">Area di testo</span><span class="sxs-lookup"><span data-stu-id="24f35-265">Text Area</span></span> |<span data-ttu-id="24f35-266">String</span><span class="sxs-lookup"><span data-stu-id="24f35-266">String</span></span> |
| <span data-ttu-id="24f35-267">Area di testo (Long)</span><span class="sxs-lookup"><span data-stu-id="24f35-267">Text Area (Long)</span></span> |<span data-ttu-id="24f35-268">String</span><span class="sxs-lookup"><span data-stu-id="24f35-268">String</span></span> |
| <span data-ttu-id="24f35-269">Area di testo (Rich)</span><span class="sxs-lookup"><span data-stu-id="24f35-269">Text Area (Rich)</span></span> |<span data-ttu-id="24f35-270">String</span><span class="sxs-lookup"><span data-stu-id="24f35-270">String</span></span> |
| <span data-ttu-id="24f35-271">Testo (Crittografato)</span><span class="sxs-lookup"><span data-stu-id="24f35-271">Text (Encrypted)</span></span> |<span data-ttu-id="24f35-272">String</span><span class="sxs-lookup"><span data-stu-id="24f35-272">String</span></span> |
| <span data-ttu-id="24f35-273">URL</span><span class="sxs-lookup"><span data-stu-id="24f35-273">URL</span></span> |<span data-ttu-id="24f35-274">String</span><span class="sxs-lookup"><span data-stu-id="24f35-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="24f35-275">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="24f35-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="24f35-276">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="24f35-276">Performance and tuning</span></span>
<span data-ttu-id="24f35-277">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md) .</span><span class="sxs-lookup"><span data-stu-id="24f35-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
