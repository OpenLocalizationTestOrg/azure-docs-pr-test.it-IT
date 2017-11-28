---
title: aaaCopy tooand di dati dall'archivio Azure Data Lake | Documenti Microsoft
description: Informazioni su come toocopy tooand di dati dall'archivio Data Lake tramite Data Factory di Azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="8b776-103">Copiare i dati tooand dall'archivio Data Lake tramite Data Factory</span><span class="sxs-lookup"><span data-stu-id="8b776-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="8b776-104">Questo articolo viene illustrato come toouse attività di copia in Azure Data Factory toomove dati tooand dall'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b776-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="8b776-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, una panoramica di spostamento dei dati con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="8b776-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8b776-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="8b776-106">Supported scenarios</span></span>
<span data-ttu-id="8b776-107">È possibile copiare dati **dall'archivio Azure Data Lake** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b776-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="8b776-108">È possibile copiare dati da archivi dati seguenti hello **tooAzure archivio Data Lake**:</span><span class="sxs-lookup"><span data-stu-id="8b776-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="8b776-109">Creare un account Data Lake Store prima della creazione di una pipeline con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="8b776-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="8b776-110">Per altre informazioni, vedere l'[introduzione ad Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8b776-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="8b776-111">Tipi di autenticazione supportati</span><span class="sxs-lookup"><span data-stu-id="8b776-111">Supported authentication types</span></span>
<span data-ttu-id="8b776-112">connettore di archivio Data Lake Hello supporta questi tipi di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="8b776-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="8b776-113">Autenticazione di un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="8b776-113">Service principal authentication</span></span>
* <span data-ttu-id="8b776-114">Autenticazione basata su credenziali dell'utente (OAuth)</span><span class="sxs-lookup"><span data-stu-id="8b776-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="8b776-115">È consigliabile usare l'autenticazione basata su entità servizio, in particolare per una copia di dati pianificata.</span><span class="sxs-lookup"><span data-stu-id="8b776-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="8b776-116">Con l'autenticazione basata sulle credenziali dell'utente può verificarsi la scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="8b776-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="8b776-117">Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="8b776-118">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="8b776-118">Get started</span></span>
<span data-ttu-id="8b776-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso Azure Data Lake Store usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="8b776-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="8b776-120">toocreate modo più semplice di Hello toocopy una pipeline di dati è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="8b776-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="8b776-121">Per un'esercitazione sulla creazione di una pipeline mediante Copia guidata hello, vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8b776-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="8b776-122">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="8b776-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8b776-123">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="8b776-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="8b776-124">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b776-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="8b776-125">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="8b776-125">Create a **data factory**.</span></span> <span data-ttu-id="8b776-126">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b776-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="8b776-127">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="8b776-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="8b776-128">Se, ad esempio, si copiano dati da un tooan di archiviazione blob di Azure archivio Azure Data Lake, due toolink servizi collegati creare l'account di archiviazione di Azure e la data factory di Azure Data Lake archivio tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b776-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="8b776-129">Per le proprietà di servizio collegato che sono specifici tooAzure archivio Data Lake, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="8b776-130">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="8b776-131">Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="8b776-132">E si crea un altro set di dati toospecify hello cartella e il percorso nell'archivio Data Lake hello che contiene dati hello copiati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="8b776-133">Per le proprietà di set di dati che sono specifici tooAzure archivio Data Lake, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="8b776-134">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="8b776-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="8b776-135">Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e AzureDataLakeStoreSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="8b776-136">Analogamente, se si sta copiando l'archivio Azure Data Lake tooAzure nell'archiviazione Blob, utilizzare AzureDataLakeStoreSource e BlobSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="8b776-137">Per le proprietà di attività di copia che sono specifici tooAzure archivio Data Lake, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="8b776-138">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="8b776-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="8b776-139">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="8b776-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="8b776-140">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b776-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="8b776-141">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati dati da e verso un archivio Azure Data Lake, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="8b776-142">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooData Lake archivio.</span><span class="sxs-lookup"><span data-stu-id="8b776-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8b776-143">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="8b776-143">Linked service properties</span></span>
<span data-ttu-id="8b776-144">Un servizio collegato di collegare una data factory tooa archivio di dati.</span><span class="sxs-lookup"><span data-stu-id="8b776-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="8b776-145">Creare un servizio collegato di tipo **AzureDataLakeStore** toolink la data factory tooyour dati di archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b776-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="8b776-146">Hello nella tabella seguente vengono descritti i servizi tooData Lake archivio collegato specifici di JSON elementi.</span><span class="sxs-lookup"><span data-stu-id="8b776-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="8b776-147">È possibile scegliere tra l'autenticazione basata su entità servizio e l'autenticazione basata su credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="8b776-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="8b776-148">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b776-148">Property</span></span> | <span data-ttu-id="8b776-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b776-149">Description</span></span> | <span data-ttu-id="8b776-150">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b776-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b776-151">**type**</span><span class="sxs-lookup"><span data-stu-id="8b776-151">**type**</span></span> | <span data-ttu-id="8b776-152">proprietà di tipo Hello deve essere impostata troppo**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="8b776-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="8b776-153">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-153">Yes</span></span> |
| <span data-ttu-id="8b776-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="8b776-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="8b776-155">Informazioni sull'account archivio Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="8b776-156">Queste informazioni accetta uno dei seguenti formati hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="8b776-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="8b776-157">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-157">Yes</span></span> |
| <span data-ttu-id="8b776-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="8b776-158">**subscriptionId**</span></span> | <span data-ttu-id="8b776-159">Hello toowhich di ID sottoscrizione di Azure account archivio Data Lake appartiene.</span><span class="sxs-lookup"><span data-stu-id="8b776-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="8b776-160">Richiesto per il sink</span><span class="sxs-lookup"><span data-stu-id="8b776-160">Required for sink</span></span> |
| <span data-ttu-id="8b776-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="8b776-161">**resourceGroupName**</span></span> | <span data-ttu-id="8b776-162">Hello toowhich di nome gruppo risorse di Azure account archivio Data Lake appartiene.</span><span class="sxs-lookup"><span data-stu-id="8b776-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="8b776-163">Richiesto per il sink</span><span class="sxs-lookup"><span data-stu-id="8b776-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="8b776-164">Autenticazione basata su entità servizio (opzione consigliata)</span><span class="sxs-lookup"><span data-stu-id="8b776-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="8b776-165">toouse l'autenticazione dell'entità servizio, registrare un'entità di applicazione in Azure Active Directory (Azure AD) e concedere hello accedere all'archivio Lake tooData.</span><span class="sxs-lookup"><span data-stu-id="8b776-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="8b776-166">Per la procedura dettaglia, vedere [Autenticazione da servizio a servizio](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8b776-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="8b776-167">Prendere nota dei seguenti valori, che permette di hello hello toodefine servizio collegato:</span><span class="sxs-lookup"><span data-stu-id="8b776-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="8b776-168">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="8b776-168">Application ID</span></span>
* <span data-ttu-id="8b776-169">Chiave applicazione</span><span class="sxs-lookup"><span data-stu-id="8b776-169">Application key</span></span> 
* <span data-ttu-id="8b776-170">ID tenant</span><span class="sxs-lookup"><span data-stu-id="8b776-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b776-171">Se si utilizza una pipeline di dati tooauthor Copia guidata hello, assicurarsi che la concessione delle entità servizio hello almeno un **lettore** ruolo di controllo di accesso (gestione delle identità e accesso) per l'account archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="8b776-172">Inoltre, concedere almeno un'entità servizio hello **lettura + Execute** autorizzazione tooyour archivio Data Lake radice ("/") e nei relativi elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="8b776-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="8b776-173">In caso contrario si potrebbe vedere il messaggio hello "hello credenziali specificate non sono validi".</span><span class="sxs-lookup"><span data-stu-id="8b776-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="8b776-174">Dopo aver creato o aggiornare un'entità servizio in Azure AD, può richiedere alcuni minuti per effetto di tootake modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="8b776-175">Controllare l'entità servizio hello e le configurazioni di archivio Data Lake accesso controllo elenco (ACL).</span><span class="sxs-lookup"><span data-stu-id="8b776-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="8b776-176">Se viene ancora visualizzato il messaggio hello "hello credenziali specificate non sono validi", attendere qualche minuto e riprovare.</span><span class="sxs-lookup"><span data-stu-id="8b776-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="8b776-177">Utilizzare l'autenticazione dell'entità servizio specificando hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b776-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="8b776-178">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b776-178">Property</span></span> | <span data-ttu-id="8b776-179">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b776-179">Description</span></span> | <span data-ttu-id="8b776-180">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b776-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b776-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="8b776-181">**servicePrincipalId**</span></span> | <span data-ttu-id="8b776-182">Specificare un ID client. dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="8b776-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="8b776-183">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-183">Yes</span></span> |
| <span data-ttu-id="8b776-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="8b776-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="8b776-185">Specificare la chiave dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-185">Specify hello application's key.</span></span> | <span data-ttu-id="8b776-186">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-186">Yes</span></span> |
| <span data-ttu-id="8b776-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="8b776-187">**tenant**</span></span> | <span data-ttu-id="8b776-188">Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b776-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="8b776-189">È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b776-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="8b776-190">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-190">Yes</span></span> |

<span data-ttu-id="8b776-191">**Esempio: autenticazione basata su entità servizio**</span><span class="sxs-lookup"><span data-stu-id="8b776-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="8b776-192">Autenticazione basata su credenziali utente</span><span class="sxs-lookup"><span data-stu-id="8b776-192">User credential authentication</span></span>
<span data-ttu-id="8b776-193">In alternativa, è possibile utilizzare toocopy di autenticazione delle credenziali utente da o archivio Lake tooData specificando hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b776-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="8b776-194">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b776-194">Property</span></span> | <span data-ttu-id="8b776-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b776-195">Description</span></span> | <span data-ttu-id="8b776-196">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b776-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b776-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="8b776-197">**authorization**</span></span> | <span data-ttu-id="8b776-198">Fare clic su hello **Authorize** pulsante hello Editor delle Data Factory e immettere le credenziali dell'utente che assegna la proprietà toothis hello generato automaticamente autorizzazione URL.</span><span class="sxs-lookup"><span data-stu-id="8b776-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="8b776-199">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-199">Yes</span></span> |
| <span data-ttu-id="8b776-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="8b776-200">**sessionId**</span></span> | <span data-ttu-id="8b776-201">ID di sessione OAuth della sessione di autorizzazione OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="8b776-202">Ogni ID di sessione è univoco e può essere usato solo una volta.</span><span class="sxs-lookup"><span data-stu-id="8b776-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="8b776-203">Questa impostazione viene generata automaticamente quando si utilizza hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b776-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="8b776-204">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-204">Yes</span></span> |

<span data-ttu-id="8b776-205">**Esempio: autenticazione basata su credenziali utente**</span><span class="sxs-lookup"><span data-stu-id="8b776-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="8b776-206">Scadenza del token</span><span class="sxs-lookup"><span data-stu-id="8b776-206">Token expiration</span></span>
<span data-ttu-id="8b776-207">codice di autorizzazione generati utilizzando hello Hello **Authorize** pulsante scade dopo un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8b776-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="8b776-208">segue messaggio Hello significa che è scaduto il token di autenticazione hello:</span><span class="sxs-lookup"><span data-stu-id="8b776-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="8b776-209">Errore dell'operazione relativa alle credenziali: invalid_grant - AADSTS70002: Errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="8b776-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="8b776-210">AADSTS70008: hello fornito concessione di accesso è scaduto o revocato.</span><span class="sxs-lookup"><span data-stu-id="8b776-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="8b776-211">ID traccia: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID correlazione: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="8b776-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="8b776-212">Hello nella tabella seguente mostra le scadenze di hello di diversi tipi di account utente:</span><span class="sxs-lookup"><span data-stu-id="8b776-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="8b776-213">Tipo di utente</span><span class="sxs-lookup"><span data-stu-id="8b776-213">User type</span></span> | <span data-ttu-id="8b776-214">Scade dopo</span><span class="sxs-lookup"><span data-stu-id="8b776-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b776-215">Account utente *non* gestiti da Azure Active Directory (ad esempio, @hotmail.com or @live.com)</span><span class="sxs-lookup"><span data-stu-id="8b776-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="8b776-216">12 ore</span><span class="sxs-lookup"><span data-stu-id="8b776-216">12 hours</span></span> |
| <span data-ttu-id="8b776-217">Account utente gestiti da Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b776-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="8b776-218">eseguire 14 giorni dopo l'ultima sezione di hello</span><span class="sxs-lookup"><span data-stu-id="8b776-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="8b776-219">90 giorni, se viene eseguita una sezione basata su un servizio collegato OAuth almeno una volta ogni 14 giorni</span><span class="sxs-lookup"><span data-stu-id="8b776-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="8b776-220">Se si modifica la password precedente all'ora di scadenza del token hello, hello scadenza del token immediatamente.</span><span class="sxs-lookup"><span data-stu-id="8b776-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="8b776-221">Verrà visualizzato il messaggio hello indicato in precedenza in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="8b776-222">È possibile riautorizzare account hello utilizzando hello **Authorize** pulsante quando il token di hello scade hello tooredeploy servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="8b776-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="8b776-223">È anche possibile generare i valori per hello **sessionId** e **autorizzazione** hello delle proprietà a livello di codice mediante il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8b776-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


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
<span data-ttu-id="8b776-224">Per ulteriori informazioni sulle classi di Data Factory hello utilizzate nel codice hello, vedere hello [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [ Classe AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) argomenti.</span><span class="sxs-lookup"><span data-stu-id="8b776-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="8b776-225">Aggiungere un riferimento tooversion `2.9.10826.1824` di `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` per hello `WindowsFormsWebAuthenticationDialog` classe utilizzata nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="8b776-226">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="8b776-226">Dataset properties</span></span>
<span data-ttu-id="8b776-227">dati di input toorepresent un set di dati in un archivio Data Lake toospecify, impostare hello **tipo** proprietà del set di dati hello troppo**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="8b776-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="8b776-228">Set hello **linkedServiceName** proprietà del nome di toohello hello set di dati di archivio Data Lake hello servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="8b776-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="8b776-229">Per un elenco completo delle sezioni JSON e le proprietà disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8b776-230">Le sezioni di un set di dati in JSON, quali **struttura**, **disponibilità**, e **criteri**, sono simili per tutti i tipi di set di dati (ad esempio database SQL di Azure, BLOB Azure e tabelle di Azure).</span><span class="sxs-lookup"><span data-stu-id="8b776-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="8b776-231">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni come percorso e il formato dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="8b776-232">Hello **typeProperties** sezione per un set di dati di tipo **AzureDataLakeStore** contiene hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b776-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="8b776-233">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b776-233">Property</span></span> | <span data-ttu-id="8b776-234">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b776-234">Description</span></span> | <span data-ttu-id="8b776-235">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b776-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b776-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="8b776-236">**folderPath**</span></span> |<span data-ttu-id="8b776-237">Percorso toohello contenitore e della cartella in archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b776-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="8b776-238">Sì</span><span class="sxs-lookup"><span data-stu-id="8b776-238">Yes</span></span> |
| <span data-ttu-id="8b776-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="8b776-239">**fileName**</span></span> |<span data-ttu-id="8b776-240">Nome del file hello in archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b776-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="8b776-241">Hello **fileName** proprietà è facoltativa tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8b776-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="8b776-242">Se si specifica **fileName**, attività hello (inclusi copia) funziona su file specifiche hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="8b776-243">Quando **fileName** non viene specificato, copia include tutti i file **folderPath** nel set di dati input hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="8b776-244">Quando **fileName** non viene specificato per un set di dati di output e **preserveHierarchy** non viene specificato nel sink di attività, il nome di hello del file hello generato è in formato hello dati. _GUID_. txt ".</span><span class="sxs-lookup"><span data-stu-id="8b776-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="8b776-245">Ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="8b776-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="8b776-246">No</span><span class="sxs-lookup"><span data-stu-id="8b776-246">No</span></span> |
| <span data-ttu-id="8b776-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="8b776-247">**partitionedBy**</span></span> |<span data-ttu-id="8b776-248">Hello **partitionedBy** proprietà è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="8b776-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="8b776-249">È possibile utilizzare il toospecify un percorso dinamico e il nome di file per i dati delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="8b776-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="8b776-250">Ad esempio, è possibile includere parametri per ogni ora di dati in **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="8b776-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="8b776-251">Per informazioni dettagliate ed esempi, vedere [hello proprietà partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="8b776-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="8b776-252">No</span><span class="sxs-lookup"><span data-stu-id="8b776-252">No</span></span> |
| <span data-ttu-id="8b776-253">**format**</span><span class="sxs-lookup"><span data-stu-id="8b776-253">**format**</span></span> | <span data-ttu-id="8b776-254">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, e  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b776-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="8b776-255">Set hello **tipo** proprietà in **formato** tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="8b776-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="8b776-256">Per ulteriori informazioni, vedere hello [formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) sezioni hello [compressione di File e formati supportati da Azure Data Factory](data-factory-supported-file-and-compression-formats.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="8b776-257">Se si desidera toocopy file "come-è" basato su file tra archivi diversi (copia binaria), ignorare hello `format` sezione in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="8b776-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b776-258">No</span><span class="sxs-lookup"><span data-stu-id="8b776-258">No</span></span> |
| <span data-ttu-id="8b776-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="8b776-259">**compression**</span></span> | <span data-ttu-id="8b776-260">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="8b776-261">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b776-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b776-262">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="8b776-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b776-263">Per altre informazioni, vedere [File e formati di compressione supportati da Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="8b776-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b776-264">No</span><span class="sxs-lookup"><span data-stu-id="8b776-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="8b776-265">proprietà partitionedBy Hello</span><span class="sxs-lookup"><span data-stu-id="8b776-265">hello partitionedBy property</span></span>
<span data-ttu-id="8b776-266">È possibile specificare dinamica **folderPath** e **fileName** proprietà per i dati delle serie temporali con hello **partitionedBy** proprietà, funzioni di Data Factory e sistema variabili.</span><span class="sxs-lookup"><span data-stu-id="8b776-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="8b776-267">Per informazioni dettagliate, vedere hello [Data Factory di Azure - funzioni e variabili di sistema](data-factory-functions-variables.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="8b776-268">Nel seguente esempio, hello `{Slice}` viene sostituito con il valore di hello della variabile di sistema di Data Factory hello `SliceStart` in formato hello specificato (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="8b776-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="8b776-269">nome Hello `SliceStart` fa riferimento toohello ora di inizio della sezione hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="8b776-270">Hello `folderPath` proprietà è diversa per ogni sezione, come in `wikidatagateway/wikisampledataout/2014100103` o `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="8b776-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="8b776-271">Nel seguente esempio, hello anno, mese, giorno e ora di hello `SliceStart` vengono estratti in variabili distinte che vengono utilizzate da hello `folderPath` e `fileName` proprietà:</span><span class="sxs-lookup"><span data-stu-id="8b776-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="8b776-272">Per ulteriori informazioni sul set di dati di serie temporali, la pianificazione e le sezioni, vedere hello [set di dati in Azure Data Factory](data-factory-create-datasets.md) e [Data Factory di pianificazione e l'esecuzione](data-factory-scheduling-and-execution.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="8b776-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="8b776-273">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="8b776-273">Copy activity properties</span></span>
<span data-ttu-id="8b776-274">Per un elenco completo delle sezioni e le proprietà disponibili per la definizione delle attività, vedere hello [creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8b776-275">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="8b776-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="8b776-276">le proprietà disponibili nella hello Hello **typeProperties** sezione di un'attività variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="8b776-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="8b776-277">Per un'attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="8b776-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="8b776-278">**AzureDataLakeStoreSource** supporta hello seguente proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="8b776-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="8b776-279">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b776-279">Property</span></span> | <span data-ttu-id="8b776-280">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b776-280">Description</span></span> | <span data-ttu-id="8b776-281">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="8b776-281">Allowed values</span></span> | <span data-ttu-id="8b776-282">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b776-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b776-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="8b776-283">**recursive**</span></span> |<span data-ttu-id="8b776-284">Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="8b776-285">True (valore predefinito), False</span><span class="sxs-lookup"><span data-stu-id="8b776-285">True (default value), False</span></span> |<span data-ttu-id="8b776-286">No</span><span class="sxs-lookup"><span data-stu-id="8b776-286">No</span></span> |


<span data-ttu-id="8b776-287">**AzureDataLakeStoreSink** supporta hello seguenti proprietà in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="8b776-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="8b776-288">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b776-288">Property</span></span> | <span data-ttu-id="8b776-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b776-289">Description</span></span> | <span data-ttu-id="8b776-290">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="8b776-290">Allowed values</span></span> | <span data-ttu-id="8b776-291">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b776-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b776-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="8b776-292">**copyBehavior**</span></span> |<span data-ttu-id="8b776-293">Specifica il comportamento di copia hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="8b776-294"><b>PreserveHierarchy</b>: mantiene la gerarchia di file hello nella cartella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="8b776-295">percorso relativo di Hello origine toosource della cartella dei file è identico toohello percorso relativo della cartella tootarget file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8b776-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="8b776-296"><b>FlattenHierarchy</b>: tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello hello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8b776-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="8b776-297">file di destinazione Hello vengono creati con nomi generati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b776-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="8b776-298"><b>Oggetto</b>: unisce tutti i file dal file tooone cartella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="8b776-299">Se hello Nome file o un blob è specificato, il nome di file sottoposto a merge hello è nome specificato hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="8b776-300">In caso contrario, il nome di file hello viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b776-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="8b776-301">No</span><span class="sxs-lookup"><span data-stu-id="8b776-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="8b776-302">esempi ricorsivi e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8b776-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="8b776-303">In questa sezione viene descritto il comportamento risultante hello dell'operazione di copia hello per diverse combinazioni di valori ricorsiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="8b776-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="8b776-304">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="8b776-304">recursive</span></span> | <span data-ttu-id="8b776-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8b776-305">copyBehavior</span></span> | <span data-ttu-id="8b776-306">Comportamento risultante</span><span class="sxs-lookup"><span data-stu-id="8b776-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b776-307">true</span><span class="sxs-lookup"><span data-stu-id="8b776-307">true</span></span> |<span data-ttu-id="8b776-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="8b776-308">preserveHierarchy</span></span> |<span data-ttu-id="8b776-309">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8b776-310">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-310">Folder1</span></span><br/><span data-ttu-id="8b776-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-313">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8b776-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8b776-317">cartella di destinazione Hello Cartella1 viene creata con hello stessa struttura come origine di hello</span><span class="sxs-lookup"><span data-stu-id="8b776-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="8b776-318">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-318">Folder1</span></span><br/><span data-ttu-id="8b776-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-321">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="8b776-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="8b776-325">true</span><span class="sxs-lookup"><span data-stu-id="8b776-325">true</span></span> |<span data-ttu-id="8b776-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="8b776-326">flattenHierarchy</span></span> |<span data-ttu-id="8b776-327">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8b776-328">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-328">Folder1</span></span><br/><span data-ttu-id="8b776-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-331">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8b776-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8b776-335">destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="8b776-336">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-336">Folder1</span></span><br/><span data-ttu-id="8b776-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="8b776-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="8b776-338">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="8b776-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="8b776-339">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3</span><span class="sxs-lookup"><span data-stu-id="8b776-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="8b776-340">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4</span><span class="sxs-lookup"><span data-stu-id="8b776-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="8b776-341">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5</span><span class="sxs-lookup"><span data-stu-id="8b776-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="8b776-342">true</span><span class="sxs-lookup"><span data-stu-id="8b776-342">true</span></span> |<span data-ttu-id="8b776-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="8b776-343">mergeFiles</span></span> |<span data-ttu-id="8b776-344">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8b776-345">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-345">Folder1</span></span><br/><span data-ttu-id="8b776-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-348">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8b776-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8b776-352">destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="8b776-353">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-353">Folder1</span></span><br/><span data-ttu-id="8b776-354">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome file generato automaticamente</span><span class="sxs-lookup"><span data-stu-id="8b776-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="8b776-355">false</span><span class="sxs-lookup"><span data-stu-id="8b776-355">false</span></span> |<span data-ttu-id="8b776-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="8b776-356">preserveHierarchy</span></span> |<span data-ttu-id="8b776-357">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8b776-358">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-358">Folder1</span></span><br/><span data-ttu-id="8b776-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-361">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8b776-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8b776-365">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura</span><span class="sxs-lookup"><span data-stu-id="8b776-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="8b776-366">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-366">Folder1</span></span><br/><span data-ttu-id="8b776-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="8b776-369">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="8b776-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="8b776-370">false</span><span class="sxs-lookup"><span data-stu-id="8b776-370">false</span></span> |<span data-ttu-id="8b776-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="8b776-371">flattenHierarchy</span></span> |<span data-ttu-id="8b776-372">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="8b776-373">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-373">Folder1</span></span><br/><span data-ttu-id="8b776-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-376">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8b776-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8b776-380">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura</span><span class="sxs-lookup"><span data-stu-id="8b776-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="8b776-381">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-381">Folder1</span></span><br/><span data-ttu-id="8b776-382">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="8b776-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="8b776-383">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="8b776-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="8b776-384">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="8b776-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="8b776-385">false</span><span class="sxs-lookup"><span data-stu-id="8b776-385">false</span></span> |<span data-ttu-id="8b776-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="8b776-386">mergeFiles</span></span> |<span data-ttu-id="8b776-387">Per una cartella di origine Cartella1 con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8b776-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="8b776-388">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-388">Folder1</span></span><br/><span data-ttu-id="8b776-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8b776-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8b776-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8b776-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8b776-391">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8b776-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8b776-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8b776-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8b776-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8b776-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8b776-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8b776-395">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura</span><span class="sxs-lookup"><span data-stu-id="8b776-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="8b776-396">Cartella1</span><span class="sxs-lookup"><span data-stu-id="8b776-396">Folder1</span></span><br/><span data-ttu-id="8b776-397">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b776-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="8b776-398">Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="8b776-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="8b776-399">Sottocartella1 con File3, File4 e File5 non considerati.</span><span class="sxs-lookup"><span data-stu-id="8b776-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="8b776-400">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="8b776-400">Supported file and compression formats</span></span>
<span data-ttu-id="8b776-401">Per informazioni dettagliate, vedere hello [formati di File e la compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="8b776-402">Esempi JSON per la copia di dati tooand dall'archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b776-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="8b776-403">seguono esempi Hello fornisce definizioni JSON di esempio.</span><span class="sxs-lookup"><span data-stu-id="8b776-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="8b776-404">È possibile utilizzare questi toocreate di definizioni di esempio una pipeline mediante hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8b776-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8b776-405">Hello esempi viene illustrato come toocopy tooand di dati dall'archiviazione Blob di Azure e archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b776-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="8b776-406">Tuttavia, i dati possono essere copiati _direttamente_ da qualsiasi hello origini tooany di sink hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="8b776-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="8b776-407">Per ulteriori informazioni, vedere sezione hello "archivi di dati supportati e formati" in hello [spostare i dati utilizzando l'attività di copia](data-factory-data-movement-activities.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="8b776-408">Esempio: Copiare i dati da archiviazione Blob di Azure tooAzure archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b776-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="8b776-409">codice di esempio Hello in questa sezione viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="8b776-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="8b776-410">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="8b776-411">Un servizio collegato di tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="8b776-412">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="8b776-413">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="8b776-414">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8b776-415">Hello esempi mostrano come serie temporale dei dati dall'archiviazione Blob di Azure sono copiato tooData Lake archivio ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8b776-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="8b776-416">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="8b776-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="8b776-417">**Servizio collegato di Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="8b776-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="8b776-418">Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="8b776-419">**Set di dati di input del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="8b776-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="8b776-420">Nell'esempio seguente di hello, dati viene prelevati da un nuovo blob ogni ora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="8b776-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="8b776-421">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="8b776-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8b776-422">percorso della cartella Hello utilizza hello anno, mese e dell'ora di inizio hello parte relativa al giorno.</span><span class="sxs-lookup"><span data-stu-id="8b776-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="8b776-423">nome del file Hello utilizza ora hello parte hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="8b776-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="8b776-424">Hello `"external": true` impostazione informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="8b776-425">**Set di dati di output di Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="8b776-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="8b776-426">Hello nel seguente archivio Lake tooData di esempio copie dei dati.</span><span class="sxs-lookup"><span data-stu-id="8b776-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="8b776-427">I nuovi dati vengono copiati tooData Lake archivio ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8b776-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="8b776-428">**Attività di copia in una pipeline con un'origine BLOB e un sink Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="8b776-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="8b776-429">Nell'esempio seguente di hello, pipeline hello contiene un'attività di copia che è configurata toouse hello set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="8b776-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="8b776-430">attività di copia Hello è pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8b776-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="8b776-431">Nella pipeline hello definizione JSON, hello `source` tipo è stato impostato troppo`BlobSource`, hello e `sink` tipo è stato impostato troppo`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="8b776-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="8b776-432">Esempio: Copiare i dati dall'archivio Azure Data Lake tooan blob di Azure</span><span class="sxs-lookup"><span data-stu-id="8b776-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="8b776-433">codice di esempio Hello in questa sezione viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="8b776-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="8b776-434">Un servizio collegato di tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="8b776-435">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="8b776-436">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="8b776-437">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="8b776-438">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b776-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8b776-439">codice Hello copia dati delle serie temporali da archivio Data Lake tooan blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8b776-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="8b776-440">**Servizio collegato di Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="8b776-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="8b776-441">Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="8b776-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="8b776-442">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="8b776-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="8b776-443">**Set di dati di input di Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="8b776-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="8b776-444">In questo esempio, l'impostazione `"external"` troppo`true` informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="8b776-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
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
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
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
<span data-ttu-id="8b776-445">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="8b776-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="8b776-446">Nell'esempio seguente di hello, i dati vengono scritti tooa nuovo blob ogni ora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="8b776-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="8b776-447">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="8b776-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8b776-448">percorso della cartella Hello utilizza hello anno, mese, giorno e dell'ora di inizio hello sezione relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="8b776-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="8b776-449">**Attività di copia in una pipeline con un'origine Azure Data Lake Store e un sink BLOB**</span><span class="sxs-lookup"><span data-stu-id="8b776-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="8b776-450">Nell'esempio seguente di hello, pipeline hello contiene un'attività di copia che è configurata toouse hello set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="8b776-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="8b776-451">attività di copia Hello è pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="8b776-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="8b776-452">Nella pipeline hello definizione JSON, hello `source` tipo è stato impostato troppo`AzureDataLakeStoreSource`, hello e `sink` tipo è stato impostato troppo`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="8b776-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="8b776-453">Nella definizione di attività di copia hello, è anche possibile mappare le colonne di toocolumns set di dati di origine hello nel set di dati di hello sink.</span><span class="sxs-lookup"><span data-stu-id="8b776-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="8b776-454">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8b776-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8b776-455">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="8b776-455">Performance and tuning</span></span>
<span data-ttu-id="8b776-456">toolearn sui fattori di hello che influiscono sulle prestazioni delle attività di copia e la modalità toooptimize, vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="8b776-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
