---
title: Trasformare dati usando lo script U-SQL - Azure | Documentazione Microsoft
description: Informazioni su come elaborare o trasformare i dati eseguendo gli script U-SQL nel servizio di calcolo di Azure Data Lake Analytics.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="3cb96-103">Trasformare i dati eseguendo script U-SQL in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3cb96-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="3cb96-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="3cb96-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="3cb96-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="3cb96-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="3cb96-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="3cb96-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="3cb96-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="3cb96-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="3cb96-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="3cb96-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="3cb96-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3cb96-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="3cb96-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3cb96-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="3cb96-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="3cb96-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="3cb96-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3cb96-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="3cb96-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="3cb96-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="3cb96-114">Una pipeline in un'istanza di Data factory di Azure elabora i dati nei servizi di archiviazione collegati usando i servizi di calcolo collegati.</span><span class="sxs-lookup"><span data-stu-id="3cb96-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="3cb96-115">Contiene una sequenza di attività in cui ogni attività esegue una specifica operazione di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="3cb96-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="3cb96-116">Questo articolo descrive l'**attività U-SQL di Data Lake Analytics** che esegue uno script **U-SQL** in un servizio di calcolo collegato di **Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3cb96-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="3cb96-117">Creare un account di Azure Data Lake Analytics prima di creare una pipeline con un'attività U-SQL di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3cb96-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="3cb96-118">Per altre informazioni su Azure Data Lake Analytics, vedere [Introduzione ad Azure Data Lake con l'SDK .NET](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3cb96-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="3cb96-119">Per la procedura dettagliata per la creazione di una data factory, dei servizi collegati, dei set di dati e di una pipeline, vedere l' [Esercitazione: Creare la prima pipeline](data-factory-build-your-first-pipeline.md) .</span><span class="sxs-lookup"><span data-stu-id="3cb96-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="3cb96-120">Usare i frammenti JSON con l'editor di Data Factory, Visual Studio o Azure PowerShell per creare le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3cb96-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="3cb96-121">Tipi di autenticazione supportati</span><span class="sxs-lookup"><span data-stu-id="3cb96-121">Supported authentication types</span></span>
<span data-ttu-id="3cb96-122">L'attività U-SQL supporta i tipi di autenticazione in Data Lake Analytics indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="3cb96-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="3cb96-123">Autenticazione di un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="3cb96-123">Service principal authentication</span></span>
* <span data-ttu-id="3cb96-124">Autenticazione basata su credenziali dell'utente (OAuth)</span><span class="sxs-lookup"><span data-stu-id="3cb96-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="3cb96-125">È consigliabile usare l'autenticazione basata sull'entità servizio, in particolare per un'esecuzione U-SQL pianificata.</span><span class="sxs-lookup"><span data-stu-id="3cb96-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="3cb96-126">Con l'autenticazione basata sulle credenziali dell'utente può verificarsi la scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="3cb96-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="3cb96-127">Per i dettagli di configurazione, vedere la sezione [Proprietà del servizio collegato](#azure-data-lake-analytics-linked-service).</span><span class="sxs-lookup"><span data-stu-id="3cb96-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="3cb96-128">Servizio collegato di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3cb96-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="3cb96-129">Creare un servizio collegato di **Azure Data Lake Analytics** per collegare un servizio di calcolo di Azure Data Lake Analytics a una Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb96-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="3cb96-130">L'attività U-SQL di Data Lake Analytics nella pipeline fa riferimento a questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="3cb96-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="3cb96-131">La tabella seguente fornisce le descrizioni delle proprietà generiche usate nella definizione JSON.</span><span class="sxs-lookup"><span data-stu-id="3cb96-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="3cb96-132">È possibile scegliere anche tra l'autenticazione basata sull'entità servizio e l'autenticazione basata sulle credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="3cb96-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="3cb96-133">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3cb96-133">Property</span></span> | <span data-ttu-id="3cb96-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3cb96-134">Description</span></span> | <span data-ttu-id="3cb96-135">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3cb96-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cb96-136">**type**</span><span class="sxs-lookup"><span data-stu-id="3cb96-136">**type**</span></span> |<span data-ttu-id="3cb96-137">La proprietà type deve essere impostata su **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="3cb96-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="3cb96-138">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-138">Yes</span></span> |
| <span data-ttu-id="3cb96-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="3cb96-139">**accountName**</span></span> |<span data-ttu-id="3cb96-140">Nome dell'account di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3cb96-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="3cb96-141">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-141">Yes</span></span> |
| <span data-ttu-id="3cb96-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="3cb96-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="3cb96-143">URI di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3cb96-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="3cb96-144">No</span><span class="sxs-lookup"><span data-stu-id="3cb96-144">No</span></span> |
| <span data-ttu-id="3cb96-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="3cb96-145">**subscriptionId**</span></span> |<span data-ttu-id="3cb96-146">ID sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb96-146">Azure subscription id</span></span> |<span data-ttu-id="3cb96-147">No (se non specificata, viene usata la sottoscrizione della Data factory).</span><span class="sxs-lookup"><span data-stu-id="3cb96-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="3cb96-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="3cb96-148">**resourceGroupName**</span></span> |<span data-ttu-id="3cb96-149">Nome del gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb96-149">Azure resource group name</span></span> |<span data-ttu-id="3cb96-150">No (se non specificata, viene usato il gruppo di risorse di Data Factory).</span><span class="sxs-lookup"><span data-stu-id="3cb96-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="3cb96-151">Autenticazione basata su entità servizio (opzione consigliata)</span><span class="sxs-lookup"><span data-stu-id="3cb96-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="3cb96-152">Per usare l'autenticazione basata su entità servizio, registrare un'entità applicazione in Azure Active Directory (Azure AD) e concedere a tale entità l'accesso a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3cb96-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="3cb96-153">Per la procedura dettaglia, vedere [Autenticazione da servizio a servizio](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="3cb96-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="3cb96-154">Prendere nota dei valori seguenti che si usano per definire il servizio collegato:</span><span class="sxs-lookup"><span data-stu-id="3cb96-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="3cb96-155">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="3cb96-155">Application ID</span></span>
* <span data-ttu-id="3cb96-156">Chiave applicazione</span><span class="sxs-lookup"><span data-stu-id="3cb96-156">Application key</span></span> 
* <span data-ttu-id="3cb96-157">ID tenant</span><span class="sxs-lookup"><span data-stu-id="3cb96-157">Tenant ID</span></span>

<span data-ttu-id="3cb96-158">Usare l'autenticazione basata su entità servizio specificando le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="3cb96-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="3cb96-159">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3cb96-159">Property</span></span> | <span data-ttu-id="3cb96-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3cb96-160">Description</span></span> | <span data-ttu-id="3cb96-161">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3cb96-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3cb96-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="3cb96-162">**servicePrincipalId**</span></span> | <span data-ttu-id="3cb96-163">Specificare l'ID client dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3cb96-163">Specify the application's client ID.</span></span> | <span data-ttu-id="3cb96-164">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-164">Yes</span></span> |
| <span data-ttu-id="3cb96-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="3cb96-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="3cb96-166">Specificare la chiave dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3cb96-166">Specify the application's key.</span></span> | <span data-ttu-id="3cb96-167">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-167">Yes</span></span> |
| <span data-ttu-id="3cb96-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="3cb96-168">**tenant**</span></span> | <span data-ttu-id="3cb96-169">Specificare le informazioni sul tenant (nome di dominio o ID tenant) in cui si trova l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3cb96-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="3cb96-170">È possibile recuperarlo passando il cursore del mouse sull'angolo superiore destro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb96-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="3cb96-171">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-171">Yes</span></span> |

<span data-ttu-id="3cb96-172">**Esempio: autenticazione basata su entità servizio**</span><span class="sxs-lookup"><span data-stu-id="3cb96-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="3cb96-173">Autenticazione basata su credenziali utente</span><span class="sxs-lookup"><span data-stu-id="3cb96-173">User credential authentication</span></span>
<span data-ttu-id="3cb96-174">In alternativa, è possibile usare l'autenticazione delle credenziali dell'utente per Data Lake Analytics specificando le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="3cb96-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="3cb96-175">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3cb96-175">Property</span></span> | <span data-ttu-id="3cb96-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3cb96-176">Description</span></span> | <span data-ttu-id="3cb96-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3cb96-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3cb96-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="3cb96-178">**authorization**</span></span> | <span data-ttu-id="3cb96-179">Fare clic sul pulsante **Autorizza** nell'editor di Data Factory e immettere le credenziali per assegnare l'URL di autorizzazione generato automaticamente a questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="3cb96-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="3cb96-180">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-180">Yes</span></span> |
| <span data-ttu-id="3cb96-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="3cb96-181">**sessionId**</span></span> | <span data-ttu-id="3cb96-182">ID sessione OAuth dalla sessione di autorizzazione oauth.</span><span class="sxs-lookup"><span data-stu-id="3cb96-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="3cb96-183">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="3cb96-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="3cb96-184">Questa impostazione viene generata automaticamente quando si usa l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3cb96-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="3cb96-185">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-185">Yes</span></span> |

<span data-ttu-id="3cb96-186">**Esempio: autenticazione basata su credenziali utente**</span><span class="sxs-lookup"><span data-stu-id="3cb96-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="3cb96-187">Scadenza del token</span><span class="sxs-lookup"><span data-stu-id="3cb96-187">Token expiration</span></span>
<span data-ttu-id="3cb96-188">Il codice di autorizzazione generato con il pulsante **Autorizza** ha una scadenza.</span><span class="sxs-lookup"><span data-stu-id="3cb96-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="3cb96-189">Per le scadenze dei diversi tipi di account utente, vedere la tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="3cb96-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="3cb96-190">Alla **scadenza del token** di autenticazione potrebbe essere visualizzato un messaggio di errore simile al seguente: Errore dell'operazione relativa alle credenziali: invalid_grant - AADSTS70002: Errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="3cb96-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="3cb96-191">AADSTS70008: La concessione dell'accesso specificata è scaduta o è stata revocata.</span><span class="sxs-lookup"><span data-stu-id="3cb96-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="3cb96-192">ID traccia: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID correlazione: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z.</span><span class="sxs-lookup"><span data-stu-id="3cb96-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="3cb96-193">Tipo di utente</span><span class="sxs-lookup"><span data-stu-id="3cb96-193">User type</span></span> | <span data-ttu-id="3cb96-194">Scade dopo</span><span class="sxs-lookup"><span data-stu-id="3cb96-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="3cb96-195">Account utente NON gestiti da Azure Active Directory (@hotmail.com, @live.com e così via).</span><span class="sxs-lookup"><span data-stu-id="3cb96-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="3cb96-196">12 ore</span><span class="sxs-lookup"><span data-stu-id="3cb96-196">12 hours</span></span> |
| <span data-ttu-id="3cb96-197">Account utente gestiti da Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="3cb96-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="3cb96-198">14 giorni dopo l'esecuzione dell'ultima sezione.</span><span class="sxs-lookup"><span data-stu-id="3cb96-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="3cb96-199">90 giorni, se viene eseguita una sezione basata sul servizio collegato OAuth almeno una volta ogni 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="3cb96-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="3cb96-200">Per evitare/risolvere questo problema, alla **scadenza del token** ripetere l'autorizzazione usando il pulsante **Autorizza** e ridistribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="3cb96-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="3cb96-201">È anche possibile generare valori per le proprietà **sessionId** e **authorization** a livello di codice usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="3cb96-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="3cb96-202">Per informazioni dettagliate sulle classi di Data Factory usate nel codice, vedere gli argomenti [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) e [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cb96-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="3cb96-203">Aggiungere un riferimento a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll per la classe WindowsFormsWebAuthenticationDialog.</span><span class="sxs-lookup"><span data-stu-id="3cb96-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="3cb96-204">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3cb96-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="3cb96-205">Il frammento JSON seguente definisce una pipeline con un'attività U-SQL di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3cb96-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="3cb96-206">La definizione dell'attività contiene un riferimento al servizio collegato di Azure Data Lake Analytics creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3cb96-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="3cb96-207">Nella tabella seguente vengono descritti i nomi e le descrizioni delle proprietà specifiche per questa attività.</span><span class="sxs-lookup"><span data-stu-id="3cb96-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="3cb96-208">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3cb96-208">Property</span></span> | <span data-ttu-id="3cb96-209">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3cb96-209">Description</span></span> | <span data-ttu-id="3cb96-210">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3cb96-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3cb96-211">Tipo</span><span class="sxs-lookup"><span data-stu-id="3cb96-211">type</span></span> |<span data-ttu-id="3cb96-212">La proprietà type deve essere impostata su **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="3cb96-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="3cb96-213">Sì</span><span class="sxs-lookup"><span data-stu-id="3cb96-213">Yes</span></span> |
| <span data-ttu-id="3cb96-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="3cb96-214">scriptPath</span></span> |<span data-ttu-id="3cb96-215">Percorso della cartella contenente lo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3cb96-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="3cb96-216">Il nome del file distingue tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="3cb96-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="3cb96-217">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="3cb96-217">No (if you use script)</span></span> |
| <span data-ttu-id="3cb96-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="3cb96-218">scriptLinkedService</span></span> |<span data-ttu-id="3cb96-219">Servizi collegati che collegano la risorsa di archiviazione contenente lo script alla Data factory</span><span class="sxs-lookup"><span data-stu-id="3cb96-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="3cb96-220">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="3cb96-220">No (if you use script)</span></span> |
| <span data-ttu-id="3cb96-221">script</span><span class="sxs-lookup"><span data-stu-id="3cb96-221">script</span></span> |<span data-ttu-id="3cb96-222">Specificare lo script inline anziché scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="3cb96-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="3cb96-223">Ad esempio: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="3cb96-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="3cb96-224">No (se si usano le proprietà scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="3cb96-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="3cb96-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="3cb96-225">degreeOfParallelism</span></span> |<span data-ttu-id="3cb96-226">Il numero massimo di nodi usati contemporaneamente per eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="3cb96-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="3cb96-227">No</span><span class="sxs-lookup"><span data-stu-id="3cb96-227">No</span></span> |
| <span data-ttu-id="3cb96-228">priority</span><span class="sxs-lookup"><span data-stu-id="3cb96-228">priority</span></span> |<span data-ttu-id="3cb96-229">Determina quali processi rispetto a tutti gli altri disponibili nella coda devono essere selezionati per essere eseguiti per primi.</span><span class="sxs-lookup"><span data-stu-id="3cb96-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="3cb96-230">Più è basso il numero, maggiore sarà la priorità.</span><span class="sxs-lookup"><span data-stu-id="3cb96-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="3cb96-231">No</span><span class="sxs-lookup"><span data-stu-id="3cb96-231">No</span></span> |
| <span data-ttu-id="3cb96-232">parameters</span><span class="sxs-lookup"><span data-stu-id="3cb96-232">parameters</span></span> |<span data-ttu-id="3cb96-233">Parametri per lo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="3cb96-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="3cb96-234">No</span><span class="sxs-lookup"><span data-stu-id="3cb96-234">No</span></span> |
| <span data-ttu-id="3cb96-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="3cb96-235">runtimeVersion</span></span> | <span data-ttu-id="3cb96-236">Versione di runtime del motore di U-SQL da usare</span><span class="sxs-lookup"><span data-stu-id="3cb96-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="3cb96-237">No</span><span class="sxs-lookup"><span data-stu-id="3cb96-237">No</span></span> | 
| <span data-ttu-id="3cb96-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="3cb96-238">compilationMode</span></span> | <p><span data-ttu-id="3cb96-239">Modalità di compilazione di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3cb96-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="3cb96-240">Deve essere uno dei valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="3cb96-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="3cb96-241">**Semantic:** esegue solo controlli semantici e i controlli di integrità necessari.</span><span class="sxs-lookup"><span data-stu-id="3cb96-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="3cb96-242">**Full:** esegue la compilazione completa, inclusi il controllo della sintassi, l'ottimizzazione, la generazione di codice e così via.</span><span class="sxs-lookup"><span data-stu-id="3cb96-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="3cb96-243">**SingleBox:** esegue la compilazione completa, con TargetType impostato su SingleBox.</span><span class="sxs-lookup"><span data-stu-id="3cb96-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="3cb96-244">Se per questa proprietà non si specifica alcun valore, il server determina la modalità di compilazione ottimale.</span><span class="sxs-lookup"><span data-stu-id="3cb96-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="3cb96-245">No</span><span class="sxs-lookup"><span data-stu-id="3cb96-245">No</span></span> | 

<span data-ttu-id="3cb96-246">Per la definizione dello script, vedere la sezione [Definizione dello script SearchLogProcessing.txt](#sample-u-sql-script) .</span><span class="sxs-lookup"><span data-stu-id="3cb96-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="3cb96-247">Set di dati di input e output di esempio</span><span class="sxs-lookup"><span data-stu-id="3cb96-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="3cb96-248">Set di dati di input</span><span class="sxs-lookup"><span data-stu-id="3cb96-248">Input dataset</span></span>
<span data-ttu-id="3cb96-249">In questo esempio i dati di input si trovano in un archivio di Azure Data Lake (file SearchLog.tsv nella cartella datalake/input).</span><span class="sxs-lookup"><span data-stu-id="3cb96-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="3cb96-250">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="3cb96-250">Output dataset</span></span>
<span data-ttu-id="3cb96-251">In questo esempio i dati di output generati dallo script U-SQL sono memorizzati in un archivio di Azure Data Lake (cartella datalake/output).</span><span class="sxs-lookup"><span data-stu-id="3cb96-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="3cb96-252">Servizio collegato di Data Lake Store di esempio</span><span class="sxs-lookup"><span data-stu-id="3cb96-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="3cb96-253">Ecco la definizione del servizio collegato di Azure Data Lake Store di esempio usato dai set di dati di input/output.</span><span class="sxs-lookup"><span data-stu-id="3cb96-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="3cb96-254">Per la descrizione delle proprietà JSON, vedere l'articolo [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) (Spostare dati da e in Azure Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="3cb96-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="3cb96-255">Script U-SQL di esempio</span><span class="sxs-lookup"><span data-stu-id="3cb96-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="3cb96-256">I valori dei parametri **@in** e **@out** nello script U-SQL vengono passati in modo dinamico da ADF usando la sezione "parameters".</span><span class="sxs-lookup"><span data-stu-id="3cb96-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="3cb96-257">Vedere la sezione "parameters" nella definizione della pipeline.</span><span class="sxs-lookup"><span data-stu-id="3cb96-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="3cb96-258">È possibile specificare anche altre proprietà come degreeOfParallelism e priorità nella definizione della pipeline per i processi in esecuzione sul servizio Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3cb96-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="3cb96-259">Parametri dinamici</span><span class="sxs-lookup"><span data-stu-id="3cb96-259">Dynamic parameters</span></span>
<span data-ttu-id="3cb96-260">Nell'esempio di definizione di pipeline i parametri in e out vengono assegnati con valori hardcoded.</span><span class="sxs-lookup"><span data-stu-id="3cb96-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="3cb96-261">È anche possibile usare parametri dinamici.</span><span class="sxs-lookup"><span data-stu-id="3cb96-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="3cb96-262">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3cb96-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="3cb96-263">In questo caso, i file di input vengono prelevati dalla cartella /datalake/input e i file di output vengono generati nella cartella /datalake/output.</span><span class="sxs-lookup"><span data-stu-id="3cb96-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="3cb96-264">I nomi dei file sono dinamici e si basano sull'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="3cb96-264">The file names are dynamic based on the slice start time.</span></span>  

