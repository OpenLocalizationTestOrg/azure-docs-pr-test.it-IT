---
title: gli endpoint REST aaaCall con HTTP + Swagger connettore per le app di logica di Azure | Documenti Microsoft
description: Connettersi tooREST endpoint da App per la logica tramite Swagger con hello HTTP + connettore Swagger
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="6ce90-103">Introduzione a salve HTTP + azione Swagger</span><span class="sxs-lookup"><span data-stu-id="6ce90-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="6ce90-104">È possibile creare un endpoint REST di prima classe connettore tooany tramite un [Swagger documento](https://swagger.io) quando si Usa HTTP hello + Swagger azione nel flusso di lavoro logica app.</span><span class="sxs-lookup"><span data-stu-id="6ce90-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="6ce90-105">È anche possibile estendere la logica App toocall qualsiasi endpoint REST con un'esperienza di progettazione applicazione la logica di prima classe.</span><span class="sxs-lookup"><span data-stu-id="6ce90-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="6ce90-106">toolearn toocreate logica App con i connettori, vedere [crea una nuova app logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6ce90-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="6ce90-107">Usare HTTP + Swagger come trigger o azione</span><span class="sxs-lookup"><span data-stu-id="6ce90-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="6ce90-108">salve HTTP + Swagger trigger e action lavoro hello stesso come hello [azione HTTP](connectors-native-http.md) , ma forniscono una migliore esperienza di progettazione applicazione logica esponendo struttura hello API e gli output di hello [metadati Swagger](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="6ce90-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="6ce90-109">È inoltre possibile utilizzare hello HTTP + connettore Swagger come trigger.</span><span class="sxs-lookup"><span data-stu-id="6ce90-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="6ce90-110">Se si vuole tooimplement un trigger di polling, seguire il polling di hello modello descritto in [creare toocall API personalizzato altri sistemi, servizi e le API da logica app](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="6ce90-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="6ce90-111">Altre informazioni sui [trigger e le azioni nelle app per la logica](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ce90-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="6ce90-112">Di seguito è riportato un esempio di come toouse hello HTTP + Swagger operazione come un'azione in un flusso di lavoro in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="6ce90-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="6ce90-113">Seleziona hello **nuovo passaggio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="6ce90-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="6ce90-114">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="6ce90-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="6ce90-115">Nella casella di ricerca azione hello, digitare **swagger** hello toolist HTTP + Swagger azione.</span><span class="sxs-lookup"><span data-stu-id="6ce90-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Selezionare l'azione HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="6ce90-117">Digitare l'URL hello per un documento di Swagger:</span><span class="sxs-lookup"><span data-stu-id="6ce90-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="6ce90-118">toowork da hello progettazione logica App hello URL deve essere un endpoint HTTPS e avere abilitata la condivisione CORS.</span><span class="sxs-lookup"><span data-stu-id="6ce90-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="6ce90-119">Se il documento di Swagger hello non soddisfa questo requisito, è possibile utilizzare [archiviazione di Azure con CORS abilitato](#hosting-swagger-from-storage) documento hello toostore.</span><span class="sxs-lookup"><span data-stu-id="6ce90-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="6ce90-120">Fare clic su **Avanti** tooread e rendering da hello Swagger documento.</span><span class="sxs-lookup"><span data-stu-id="6ce90-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="6ce90-121">Aggiungere i parametri necessari per la chiamata hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ce90-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Completare l'azione HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="6ce90-123">toosave e pubblicare l'app logica, fare clic su **salvare** sulla barra degli strumenti della finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="6ce90-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="6ce90-124">Ospitare Swagger da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6ce90-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="6ce90-125">È possibile tooreference un documento di Swagger che non è ospitato o che non soddisfa i requisiti di sicurezza e cross-origin hello per progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="6ce90-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="6ce90-126">tooresolve questo problema, è possibile archiviare documenti Swagger hello in archiviazione di Azure e abilitare CORS tooreference hello documenti.</span><span class="sxs-lookup"><span data-stu-id="6ce90-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="6ce90-127">Di seguito sono toocreate passaggi hello, configurare e archiviare documenti Swagger in archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="6ce90-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="6ce90-128">[Creare un account di Archiviazione di Azure con Archiviazione BLOB di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6ce90-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="6ce90-129">tooperform questo passaggio, impostazione delle autorizzazioni troppo**accesso pubblico**.</span><span class="sxs-lookup"><span data-stu-id="6ce90-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="6ce90-130">Abilitare CORS nel blob hello.</span><span class="sxs-lookup"><span data-stu-id="6ce90-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="6ce90-131">tooautomatically configurare questa impostazione, è possibile utilizzare [questo script di PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="6ce90-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="6ce90-132">Caricare blob toohello file Swagger di hello.</span><span class="sxs-lookup"><span data-stu-id="6ce90-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="6ce90-133">È possibile eseguire questo passaggio da hello [portale di Azure](https://portal.azure.com) o da uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6ce90-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="6ce90-134">Fare riferimento a un documento di toohello collegamento HTTPS nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce90-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="6ce90-135">collegamento Hello viene utilizzato questo formato:</span><span class="sxs-lookup"><span data-stu-id="6ce90-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="6ce90-136">Dettagli tecnici</span><span class="sxs-lookup"><span data-stu-id="6ce90-136">Technical details</span></span>
<span data-ttu-id="6ce90-137">Di seguito sono hello i dettagli per azioni e trigger hello da questo HTTP + Swagger connettore supporta.</span><span class="sxs-lookup"><span data-stu-id="6ce90-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="6ce90-138">Trigger HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="6ce90-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="6ce90-139">Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="6ce90-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="6ce90-140">Altre informazioni sui trigger.</span><span class="sxs-lookup"><span data-stu-id="6ce90-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="6ce90-141">Hello HTTP + Swagger connettore dispone di un trigger.</span><span class="sxs-lookup"><span data-stu-id="6ce90-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="6ce90-142">Trigger</span><span class="sxs-lookup"><span data-stu-id="6ce90-142">Trigger</span></span> | <span data-ttu-id="6ce90-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ce90-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ce90-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="6ce90-144">HTTP + Swagger</span></span> |<span data-ttu-id="6ce90-145">Effettuare una chiamata HTTP e restituiscono contenuto della risposta hello</span><span class="sxs-lookup"><span data-stu-id="6ce90-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="6ce90-146">Azioni HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="6ce90-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="6ce90-147">Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="6ce90-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="6ce90-148">Ulteriori informazioni sulle azioni.</span><span class="sxs-lookup"><span data-stu-id="6ce90-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="6ce90-149">Hello HTTP + Swagger connettore dispone di un'azione possibile.</span><span class="sxs-lookup"><span data-stu-id="6ce90-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="6ce90-150">Azione</span><span class="sxs-lookup"><span data-stu-id="6ce90-150">Action</span></span> | <span data-ttu-id="6ce90-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ce90-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ce90-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="6ce90-152">HTTP + Swagger</span></span> |<span data-ttu-id="6ce90-153">Effettuare una chiamata HTTP e restituiscono contenuto della risposta hello</span><span class="sxs-lookup"><span data-stu-id="6ce90-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="6ce90-154">Informazioni dettagliate sulle azioni</span><span class="sxs-lookup"><span data-stu-id="6ce90-154">Action details</span></span>
<span data-ttu-id="6ce90-155">Hello HTTP + Swagger connettore viene fornito con un'azione possibile.</span><span class="sxs-lookup"><span data-stu-id="6ce90-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="6ce90-156">Di seguito è informazioni su ognuna delle azioni di hello, i relativi campi di input obbligatori e facoltativi e hello corrispondente dettagli output associati al loro utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6ce90-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="6ce90-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="6ce90-157">HTTP + Swagger</span></span>
<span data-ttu-id="6ce90-158">Eseguire una richiesta HTTP in uscita con l'assistenza dei metadati Swagger.</span><span class="sxs-lookup"><span data-stu-id="6ce90-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="6ce90-159">L'asterisco (*) indica un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="6ce90-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="6ce90-160">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="6ce90-160">Display name</span></span> | <span data-ttu-id="6ce90-161">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="6ce90-161">Property name</span></span> | <span data-ttu-id="6ce90-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ce90-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ce90-163">Metodo*</span><span class="sxs-lookup"><span data-stu-id="6ce90-163">Method*</span></span> |<span data-ttu-id="6ce90-164">statico</span><span class="sxs-lookup"><span data-stu-id="6ce90-164">method</span></span> |<span data-ttu-id="6ce90-165">Toouse verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ce90-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="6ce90-166">URI*</span><span class="sxs-lookup"><span data-stu-id="6ce90-166">URI*</span></span> |<span data-ttu-id="6ce90-167">Uri</span><span class="sxs-lookup"><span data-stu-id="6ce90-167">uri</span></span> |<span data-ttu-id="6ce90-168">URI di richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="6ce90-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="6ce90-169">Headers</span><span class="sxs-lookup"><span data-stu-id="6ce90-169">Headers</span></span> |<span data-ttu-id="6ce90-170">headers</span><span class="sxs-lookup"><span data-stu-id="6ce90-170">headers</span></span> |<span data-ttu-id="6ce90-171">Oggetto JSON di tooinclude intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ce90-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="6ce90-172">Corpo</span><span class="sxs-lookup"><span data-stu-id="6ce90-172">Body</span></span> |<span data-ttu-id="6ce90-173">body</span><span class="sxs-lookup"><span data-stu-id="6ce90-173">body</span></span> |<span data-ttu-id="6ce90-174">Hello corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ce90-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="6ce90-175">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="6ce90-175">Authentication</span></span> |<span data-ttu-id="6ce90-176">authentication</span><span class="sxs-lookup"><span data-stu-id="6ce90-176">authentication</span></span> |<span data-ttu-id="6ce90-177">Autenticazione toouse per richiesta.</span><span class="sxs-lookup"><span data-stu-id="6ce90-177">Authentication toouse for request.</span></span> <span data-ttu-id="6ce90-178">Per ulteriori informazioni, vedere hello [connettore HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="6ce90-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="6ce90-179">**Dettagli dell'output**</span><span class="sxs-lookup"><span data-stu-id="6ce90-179">**Output details**</span></span>

<span data-ttu-id="6ce90-180">Risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="6ce90-180">HTTP response</span></span>

| <span data-ttu-id="6ce90-181">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="6ce90-181">Property Name</span></span> | <span data-ttu-id="6ce90-182">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="6ce90-182">Data type</span></span> | <span data-ttu-id="6ce90-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ce90-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ce90-184">headers</span><span class="sxs-lookup"><span data-stu-id="6ce90-184">Headers</span></span> |<span data-ttu-id="6ce90-185">object</span><span class="sxs-lookup"><span data-stu-id="6ce90-185">object</span></span> |<span data-ttu-id="6ce90-186">Intestazioni della risposta</span><span class="sxs-lookup"><span data-stu-id="6ce90-186">Response headers</span></span> |
| <span data-ttu-id="6ce90-187">Corpo</span><span class="sxs-lookup"><span data-stu-id="6ce90-187">Body</span></span> |<span data-ttu-id="6ce90-188">object</span><span class="sxs-lookup"><span data-stu-id="6ce90-188">object</span></span> |<span data-ttu-id="6ce90-189">Oggetto della risposta</span><span class="sxs-lookup"><span data-stu-id="6ce90-189">Response object</span></span> |
| <span data-ttu-id="6ce90-190">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="6ce90-190">Status Code</span></span> |<span data-ttu-id="6ce90-191">int</span><span class="sxs-lookup"><span data-stu-id="6ce90-191">int</span></span> |<span data-ttu-id="6ce90-192">Stato codice HTTP</span><span class="sxs-lookup"><span data-stu-id="6ce90-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="6ce90-193">Risposte HTTP</span><span class="sxs-lookup"><span data-stu-id="6ce90-193">HTTP responses</span></span>
<span data-ttu-id="6ce90-194">Quando si effettuano chiamate toovarious azioni, si potrebbero ottenere alcune risposte.</span><span class="sxs-lookup"><span data-stu-id="6ce90-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="6ce90-195">Di seguito è riportata una tabella contenente le risposte e le descrizioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="6ce90-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="6ce90-196">Nome</span><span class="sxs-lookup"><span data-stu-id="6ce90-196">Name</span></span> | <span data-ttu-id="6ce90-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ce90-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ce90-198">200</span><span class="sxs-lookup"><span data-stu-id="6ce90-198">200</span></span> |<span data-ttu-id="6ce90-199">OK</span><span class="sxs-lookup"><span data-stu-id="6ce90-199">OK</span></span> |
| <span data-ttu-id="6ce90-200">202</span><span class="sxs-lookup"><span data-stu-id="6ce90-200">202</span></span> |<span data-ttu-id="6ce90-201">Accepted</span><span class="sxs-lookup"><span data-stu-id="6ce90-201">Accepted</span></span> |
| <span data-ttu-id="6ce90-202">400</span><span class="sxs-lookup"><span data-stu-id="6ce90-202">400</span></span> |<span data-ttu-id="6ce90-203">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="6ce90-203">Bad request</span></span> |
| <span data-ttu-id="6ce90-204">401</span><span class="sxs-lookup"><span data-stu-id="6ce90-204">401</span></span> |<span data-ttu-id="6ce90-205">Non autorizzata</span><span class="sxs-lookup"><span data-stu-id="6ce90-205">Unauthorized</span></span> |
| <span data-ttu-id="6ce90-206">403</span><span class="sxs-lookup"><span data-stu-id="6ce90-206">403</span></span> |<span data-ttu-id="6ce90-207">Accesso negato</span><span class="sxs-lookup"><span data-stu-id="6ce90-207">Forbidden</span></span> |
| <span data-ttu-id="6ce90-208">404</span><span class="sxs-lookup"><span data-stu-id="6ce90-208">404</span></span> |<span data-ttu-id="6ce90-209">Non trovato</span><span class="sxs-lookup"><span data-stu-id="6ce90-209">Not Found</span></span> |
| <span data-ttu-id="6ce90-210">500</span><span class="sxs-lookup"><span data-stu-id="6ce90-210">500</span></span> |<span data-ttu-id="6ce90-211">Errore interno del server.</span><span class="sxs-lookup"><span data-stu-id="6ce90-211">Internal server error.</span></span> <span data-ttu-id="6ce90-212">Si è verificato un errore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="6ce90-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="6ce90-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ce90-213">Next steps</span></span>

* [<span data-ttu-id="6ce90-214">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="6ce90-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="6ce90-215">Trovare altri connettori</span><span class="sxs-lookup"><span data-stu-id="6ce90-215">Find other connectors</span></span>](apis-list.md)