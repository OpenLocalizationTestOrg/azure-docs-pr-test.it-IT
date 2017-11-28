---
title: dati aaaTransform utilizzando lo script U-SQL - Azure | Documenti Microsoft
description: Informazioni su come servizio di calcolo tooprocess o la trasformazione dei dati eseguendo gli script U-SQL in Azure Data Lake Analitica.
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
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="aa762-103">Trasformare i dati eseguendo script U-SQL in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="aa762-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="aa762-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="aa762-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="aa762-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="aa762-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="aa762-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="aa762-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="aa762-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="aa762-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="aa762-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="aa762-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="aa762-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa762-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="aa762-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa762-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="aa762-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="aa762-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="aa762-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="aa762-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="aa762-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="aa762-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="aa762-114">Una pipeline in un'istanza di Data factory di Azure elabora i dati nei servizi di archiviazione collegati usando i servizi di calcolo collegati.</span><span class="sxs-lookup"><span data-stu-id="aa762-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="aa762-115">Contiene una sequenza di attività in cui ogni attività esegue una specifica operazione di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="aa762-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="aa762-116">Questo articolo descrive hello **Data Lake Analitica U-SQL attività** che esegue un **U-SQL** script un **Azure Data Lake Analitica** servizio collegato di calcolo.</span><span class="sxs-lookup"><span data-stu-id="aa762-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="aa762-117">Creare un account di Azure Data Lake Analytics prima di creare una pipeline con un'attività U-SQL di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="aa762-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="aa762-118">toolearn su Azure Data Lake Analitica, vedere [Guida introduttiva di Azure Data Lake Analitica](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aa762-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="aa762-119">Hello revisione [compilare la prima esercitazione di pipeline](data-factory-build-your-first-pipeline.md) per i passaggi dettagliati toocreate una data factory, collegato a una pipeline, i set di dati e servizi.</span><span class="sxs-lookup"><span data-stu-id="aa762-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="aa762-120">Usare i frammenti di codice JSON con l'Editor delle Data Factory o le entità di Visual Studio o PowerShell di Azure Data Factory di toocreate.</span><span class="sxs-lookup"><span data-stu-id="aa762-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="aa762-121">Tipi di autenticazione supportati</span><span class="sxs-lookup"><span data-stu-id="aa762-121">Supported authentication types</span></span>
<span data-ttu-id="aa762-122">L'attività U-SQL supporta i tipi di autenticazione in Data Lake Analytics indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="aa762-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="aa762-123">Autenticazione di un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="aa762-123">Service principal authentication</span></span>
* <span data-ttu-id="aa762-124">Autenticazione basata su credenziali dell'utente (OAuth)</span><span class="sxs-lookup"><span data-stu-id="aa762-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="aa762-125">È consigliabile usare l'autenticazione basata sull'entità servizio, in particolare per un'esecuzione U-SQL pianificata.</span><span class="sxs-lookup"><span data-stu-id="aa762-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="aa762-126">Con l'autenticazione basata sulle credenziali dell'utente può verificarsi la scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="aa762-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="aa762-127">Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#azure-data-lake-analytics-linked-service) sezione.</span><span class="sxs-lookup"><span data-stu-id="aa762-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="aa762-128">Servizio collegato di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="aa762-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="aa762-129">Si crea un **Azure Data Lake Analitica** collegato servizio toolink una factory di dati di Azure tooan del servizio di calcolo di Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="aa762-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="aa762-130">attività Data Lake Analitica U-SQL nella pipeline hello Hello fa riferimento a servizio toothis collegato.</span><span class="sxs-lookup"><span data-stu-id="aa762-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="aa762-131">Hello nella tabella seguente vengono fornite descrizioni per hello generica proprietà utilizzate nella definizione JSON hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="aa762-132">È possibile scegliere anche tra l'autenticazione basata sull'entità servizio e l'autenticazione basata sulle credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="aa762-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="aa762-133">Proprietà</span><span class="sxs-lookup"><span data-stu-id="aa762-133">Property</span></span> | <span data-ttu-id="aa762-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aa762-134">Description</span></span> | <span data-ttu-id="aa762-135">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="aa762-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aa762-136">**type**</span><span class="sxs-lookup"><span data-stu-id="aa762-136">**type**</span></span> |<span data-ttu-id="aa762-137">proprietà di tipo Hello deve essere impostata su: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="aa762-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="aa762-138">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-138">Yes</span></span> |
| <span data-ttu-id="aa762-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="aa762-139">**accountName**</span></span> |<span data-ttu-id="aa762-140">Nome dell'account di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="aa762-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="aa762-141">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-141">Yes</span></span> |
| <span data-ttu-id="aa762-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="aa762-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="aa762-143">URI di Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="aa762-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="aa762-144">No</span><span class="sxs-lookup"><span data-stu-id="aa762-144">No</span></span> |
| <span data-ttu-id="aa762-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="aa762-145">**subscriptionId**</span></span> |<span data-ttu-id="aa762-146">ID sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="aa762-146">Azure subscription id</span></span> |<span data-ttu-id="aa762-147">No (se non specificato, sottoscrizione di hello viene utilizzata una data factory).</span><span class="sxs-lookup"><span data-stu-id="aa762-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="aa762-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="aa762-148">**resourceGroupName**</span></span> |<span data-ttu-id="aa762-149">Nome del gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="aa762-149">Azure resource group name</span></span> |<span data-ttu-id="aa762-150">No (se non specificato, il gruppo di risorse di hello viene utilizzata una data factory).</span><span class="sxs-lookup"><span data-stu-id="aa762-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="aa762-151">Autenticazione basata su entità servizio (opzione consigliata)</span><span class="sxs-lookup"><span data-stu-id="aa762-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="aa762-152">toouse l'autenticazione dell'entità servizio, registrare un'entità di applicazione in Azure Active Directory (Azure AD) e concedere hello accedere all'archivio Lake tooData.</span><span class="sxs-lookup"><span data-stu-id="aa762-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="aa762-153">Per la procedura dettaglia, vedere [Autenticazione da servizio a servizio](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="aa762-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="aa762-154">Prendere nota dei seguenti valori, che permette di hello hello toodefine servizio collegato:</span><span class="sxs-lookup"><span data-stu-id="aa762-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="aa762-155">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="aa762-155">Application ID</span></span>
* <span data-ttu-id="aa762-156">Chiave applicazione</span><span class="sxs-lookup"><span data-stu-id="aa762-156">Application key</span></span> 
* <span data-ttu-id="aa762-157">ID tenant</span><span class="sxs-lookup"><span data-stu-id="aa762-157">Tenant ID</span></span>

<span data-ttu-id="aa762-158">Utilizzare l'autenticazione dell'entità servizio specificando hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa762-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="aa762-159">Proprietà</span><span class="sxs-lookup"><span data-stu-id="aa762-159">Property</span></span> | <span data-ttu-id="aa762-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aa762-160">Description</span></span> | <span data-ttu-id="aa762-161">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="aa762-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa762-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="aa762-162">**servicePrincipalId**</span></span> | <span data-ttu-id="aa762-163">Specificare un ID client. dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="aa762-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="aa762-164">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-164">Yes</span></span> |
| <span data-ttu-id="aa762-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="aa762-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="aa762-166">Specificare la chiave dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-166">Specify hello application's key.</span></span> | <span data-ttu-id="aa762-167">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-167">Yes</span></span> |
| <span data-ttu-id="aa762-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="aa762-168">**tenant**</span></span> | <span data-ttu-id="aa762-169">Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa762-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="aa762-170">È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa762-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="aa762-171">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-171">Yes</span></span> |

<span data-ttu-id="aa762-172">**Esempio: autenticazione basata su entità servizio**</span><span class="sxs-lookup"><span data-stu-id="aa762-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="aa762-173">Autenticazione basata su credenziali utente</span><span class="sxs-lookup"><span data-stu-id="aa762-173">User credential authentication</span></span>
<span data-ttu-id="aa762-174">In alternativa, è possibile utilizzare l'autenticazione delle credenziali utente per Data Lake Analitica specificando hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa762-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="aa762-175">Proprietà</span><span class="sxs-lookup"><span data-stu-id="aa762-175">Property</span></span> | <span data-ttu-id="aa762-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aa762-176">Description</span></span> | <span data-ttu-id="aa762-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="aa762-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa762-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="aa762-178">**authorization**</span></span> | <span data-ttu-id="aa762-179">Fare clic su hello **Authorize** pulsante hello Editor delle Data Factory e immettere le credenziali dell'utente che assegna la proprietà toothis hello generato automaticamente autorizzazione URL.</span><span class="sxs-lookup"><span data-stu-id="aa762-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="aa762-180">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-180">Yes</span></span> |
| <span data-ttu-id="aa762-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="aa762-181">**sessionId**</span></span> | <span data-ttu-id="aa762-182">ID di sessione OAuth della sessione di autorizzazione OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="aa762-183">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="aa762-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="aa762-184">Questa impostazione viene generata automaticamente quando si utilizza hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aa762-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="aa762-185">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-185">Yes</span></span> |

<span data-ttu-id="aa762-186">**Esempio: autenticazione basata su credenziali utente**</span><span class="sxs-lookup"><span data-stu-id="aa762-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="aa762-187">Scadenza del token</span><span class="sxs-lookup"><span data-stu-id="aa762-187">Token expiration</span></span>
<span data-ttu-id="aa762-188">codice di autorizzazione è stato generato utilizzando hello Hello **Authorize** pulsante scade dopo qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="aa762-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="aa762-189">Vedere hello nella tabella seguente per date di scadenza hello per diversi tipi di account utente.</span><span class="sxs-lookup"><span data-stu-id="aa762-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="aa762-190">Si può vedere hello seguente messaggio di errore hello quando l'autenticazione **scadenza del token**: errore nell'operazione di credenziali: invalid_grant - AADSTS70002: errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="aa762-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="aa762-191">AADSTS70008: hello fornito concessione di accesso è scaduto o revocato.</span><span class="sxs-lookup"><span data-stu-id="aa762-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="aa762-192">ID traccia: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID correlazione: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z.</span><span class="sxs-lookup"><span data-stu-id="aa762-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="aa762-193">Tipo di utente</span><span class="sxs-lookup"><span data-stu-id="aa762-193">User type</span></span> | <span data-ttu-id="aa762-194">Scade dopo</span><span class="sxs-lookup"><span data-stu-id="aa762-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="aa762-195">Account utente NON gestiti da Azure Active Directory (@hotmail.com, @live.com e così via).</span><span class="sxs-lookup"><span data-stu-id="aa762-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="aa762-196">12 ore</span><span class="sxs-lookup"><span data-stu-id="aa762-196">12 hours</span></span> |
| <span data-ttu-id="aa762-197">Account utente gestiti da Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="aa762-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="aa762-198">eseguire 14 giorni dopo l'ultima sezione di hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="aa762-199">90 giorni, se viene eseguita una sezione basata sul servizio collegato OAuth almeno una volta ogni 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="aa762-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="aa762-200">tooavoid e risolvere questo errore, riautorizzare utilizzando hello **Authorize** pulsante quando hello **scadenza del token** e ridistribuire il servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="aa762-201">È anche possibile generare valori per le proprietà **sessionId** e **authorization** a livello di codice usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aa762-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="aa762-202">Vedere [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) argomenti per informazioni dettagliate informazioni sulle classi di Data Factory hello usate nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="aa762-203">Aggiungere un riferimento a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll per hello WindowsFormsWebAuthenticationDialog classe.</span><span class="sxs-lookup"><span data-stu-id="aa762-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="aa762-204">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="aa762-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="aa762-205">Hello frammento di codice JSON seguente definisce una pipeline con attività Data Lake Analitica U-SQL.</span><span class="sxs-lookup"><span data-stu-id="aa762-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="aa762-206">definizione di attività Hello è toohello un riferimento del servizio Azure Data Lake Analitica collegato, creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="aa762-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="aa762-207">Hello nella tabella seguente descrive i nomi e le descrizioni delle proprietà che sono attività toothis specifico.</span><span class="sxs-lookup"><span data-stu-id="aa762-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="aa762-208">Proprietà</span><span class="sxs-lookup"><span data-stu-id="aa762-208">Property</span></span> | <span data-ttu-id="aa762-209">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aa762-209">Description</span></span> | <span data-ttu-id="aa762-210">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="aa762-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa762-211">type</span><span class="sxs-lookup"><span data-stu-id="aa762-211">type</span></span> |<span data-ttu-id="aa762-212">proprietà di tipo Hello deve essere impostata troppo**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="aa762-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="aa762-213">Sì</span><span class="sxs-lookup"><span data-stu-id="aa762-213">Yes</span></span> |
| <span data-ttu-id="aa762-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="aa762-214">scriptPath</span></span> |<span data-ttu-id="aa762-215">Toofolder percorso che contiene lo script hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="aa762-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="aa762-216">Nome del file hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="aa762-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="aa762-217">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="aa762-217">No (if you use script)</span></span> |
| <span data-ttu-id="aa762-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="aa762-218">scriptLinkedService</span></span> |<span data-ttu-id="aa762-219">Servizio collegato che si collega archiviazione hello che contiene una data factory di hello script toohello</span><span class="sxs-lookup"><span data-stu-id="aa762-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="aa762-220">No (se si usa uno script)</span><span class="sxs-lookup"><span data-stu-id="aa762-220">No (if you use script)</span></span> |
| <span data-ttu-id="aa762-221">script</span><span class="sxs-lookup"><span data-stu-id="aa762-221">script</span></span> |<span data-ttu-id="aa762-222">Specificare lo script inline anziché scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="aa762-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="aa762-223">Ad esempio: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="aa762-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="aa762-224">No (se si usano le proprietà scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="aa762-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="aa762-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="aa762-225">degreeOfParallelism</span></span> |<span data-ttu-id="aa762-226">numero massimo di Hello di nodi utilizzati contemporaneamente processo hello toorun.</span><span class="sxs-lookup"><span data-stu-id="aa762-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="aa762-227">No</span><span class="sxs-lookup"><span data-stu-id="aa762-227">No</span></span> |
| <span data-ttu-id="aa762-228">priority</span><span class="sxs-lookup"><span data-stu-id="aa762-228">priority</span></span> |<span data-ttu-id="aa762-229">Determina innanzitutto quali processi, tra tutti quelli accodati devono essere toorun selezionato.</span><span class="sxs-lookup"><span data-stu-id="aa762-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="aa762-230">Hello hello numero inferiore, priorità più alta hello hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="aa762-231">No</span><span class="sxs-lookup"><span data-stu-id="aa762-231">No</span></span> |
| <span data-ttu-id="aa762-232">parameters</span><span class="sxs-lookup"><span data-stu-id="aa762-232">parameters</span></span> |<span data-ttu-id="aa762-233">Parametri per hello U-SQL script</span><span class="sxs-lookup"><span data-stu-id="aa762-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="aa762-234">No</span><span class="sxs-lookup"><span data-stu-id="aa762-234">No</span></span> |
| <span data-ttu-id="aa762-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="aa762-235">runtimeVersion</span></span> | <span data-ttu-id="aa762-236">Versione di runtime di toouse motore hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="aa762-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="aa762-237">No</span><span class="sxs-lookup"><span data-stu-id="aa762-237">No</span></span> | 
| <span data-ttu-id="aa762-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="aa762-238">compilationMode</span></span> | <p><span data-ttu-id="aa762-239">Modalità di compilazione di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="aa762-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="aa762-240">Deve essere uno dei valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa762-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="aa762-241">**Semantic:** esegue solo controlli semantici e i controlli di integrità necessari.</span><span class="sxs-lookup"><span data-stu-id="aa762-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="aa762-242">**Full:** eseguire una compilazione completa hello, quali controllo della sintassi, l'ottimizzazione, la generazione di codice, e così via.</span><span class="sxs-lookup"><span data-stu-id="aa762-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="aa762-243">**SingleBox:** eseguire una compilazione completa hello, con tooSingleBox di impostazione di TargetType.</span><span class="sxs-lookup"><span data-stu-id="aa762-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="aa762-244">Se non si specifica un valore per questa proprietà, il server di hello determina la modalità di compilazione ottimale hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="aa762-245">No</span><span class="sxs-lookup"><span data-stu-id="aa762-245">No</span></span> | 

<span data-ttu-id="aa762-246">Vedere [SearchLogProcessing.txt crea Script per definizione](#sample-u-sql-script) per la definizione di script hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="aa762-247">Set di dati di input e output di esempio</span><span class="sxs-lookup"><span data-stu-id="aa762-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="aa762-248">Set di dati di input</span><span class="sxs-lookup"><span data-stu-id="aa762-248">Input dataset</span></span>
<span data-ttu-id="aa762-249">In questo esempio, i dati di input hello si trovano in un archivio Azure Data Lake (SearchLog.tsv file nella cartella Lake/input hello).</span><span class="sxs-lookup"><span data-stu-id="aa762-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="aa762-250">Set di dati di output</span><span class="sxs-lookup"><span data-stu-id="aa762-250">Output dataset</span></span>
<span data-ttu-id="aa762-251">In questo esempio, i dati di output di hello prodotti da hello script U-SQL vengono archiviati in un archivio Azure Data Lake (cartella Lake/output).</span><span class="sxs-lookup"><span data-stu-id="aa762-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="aa762-252">Servizio collegato di Data Lake Store di esempio</span><span class="sxs-lookup"><span data-stu-id="aa762-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="aa762-253">Di seguito è la definizione hello dell'esempio hello che archivio Azure Data Lake collegato servizio utilizzato dal set di dati di input/output di hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

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

<span data-ttu-id="aa762-254">Vedere [spostare tooand dati dall'archivio Azure Data Lake](data-factory-azure-datalake-connector.md) articolo per una descrizione delle proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="aa762-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="aa762-255">Script U-SQL di esempio</span><span class="sxs-lookup"><span data-stu-id="aa762-255">Sample U-SQL Script</span></span>

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
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="aa762-256">i valori per Hello  **@in**  e  **@out**  parametri nello script hello U-SQL vengono passati in modo dinamico dal file ADF mediante sezione 'parameters' hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="aa762-257">Vedere la sezione 'parameters' hello definizione pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="aa762-258">È possibile specificare anche altre proprietà, ad esempio la priorità e degreeOfParallelism nella definizione di pipeline per i processi di hello eseguiti sul servizio Azure Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="aa762-259">Parametri dinamici</span><span class="sxs-lookup"><span data-stu-id="aa762-259">Dynamic parameters</span></span>
<span data-ttu-id="aa762-260">Nella definizione di pipeline di esempio hello, i parametri vengono assegnati con i valori hardcoded.</span><span class="sxs-lookup"><span data-stu-id="aa762-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="aa762-261">È invece possibile toouse dei parametri dinamici.</span><span class="sxs-lookup"><span data-stu-id="aa762-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="aa762-262">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="aa762-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="aa762-263">In questo caso, i file di input sono ancora prelevati dalla cartella /datalake/input hello e vengono generati file di output nella cartella /datalake/output hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="aa762-264">i nomi di file Hello sono dinamici in base a ora di inizio sezione hello.</span><span class="sxs-lookup"><span data-stu-id="aa762-264">hello file names are dynamic based on hello slice start time.</span></span>  

