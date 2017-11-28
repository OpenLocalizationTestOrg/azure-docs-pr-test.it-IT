---
title: Chiamare gli endpoint REST con il connettore HTTP + Swagger per le App per la logica di Azure | Microsoft Docs
description: Connettersi agli endpoint REST dalle app per la logica tramite Swagger con il connettore HTTP + Swagger
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="f58be-103">Introduzione all'azione HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="f58be-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="f58be-104">È possibile creare un connettore di prima classe a qualsiasi endpoint REST tramite un [documento di Swagger](https://swagger.io) quando si usa l'azione HTTP + Swagger nel flusso di lavoro dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f58be-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="f58be-105">È anche possibile estendere app per la logica per chiamare qualsiasi endpoint REST con un'eccellente esperienza di progettazione delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f58be-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="f58be-106">Per informazioni su come creare app per la logica con i connettori, consultare [Creare una nuova app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f58be-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="f58be-107">Usare HTTP + Swagger come trigger o azione</span><span class="sxs-lookup"><span data-stu-id="f58be-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="f58be-108">Il trigger e l'azione HTTP + Swagger funzionano come l'[azione HTTP](connectors-native-http.md), ma offrono un'esperienza migliore in Progettazione app per la logica, mostrando la forma dell'API e i risultati grazie ai [metadati Swagger](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="f58be-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="f58be-109">È anche possibile usare il connettore HTTP + Swagger come trigger.</span><span class="sxs-lookup"><span data-stu-id="f58be-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="f58be-110">Se si desidera implementare un trigger di poll, seguire il modello di polling descritto in [Creazione di un'API personalizzata da usare con le app per la logica](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="f58be-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="f58be-111">Altre informazioni sui [trigger e le azioni nelle app per la logica](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f58be-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="f58be-112">Di seguito è riportato un esempio di come usare l'operazione HTTP + Swagger come azione in un flusso di lavoro in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f58be-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="f58be-113">Fare clic sul pulsante **Nuovo passaggio** .</span><span class="sxs-lookup"><span data-stu-id="f58be-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="f58be-114">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="f58be-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="f58be-115">Nella casella di ricerca azione digitare **swagger** per elencare l'azione HTTP + Swagger.</span><span class="sxs-lookup"><span data-stu-id="f58be-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Selezionare l'azione HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="f58be-117">Digitare l'URL per un documento di Swagger:</span><span class="sxs-lookup"><span data-stu-id="f58be-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="f58be-118">Per funzionare dalla finestra di progettazione app per la logica, l'URL deve essere un endpoint HTTPS e avere CORS abilitato.</span><span class="sxs-lookup"><span data-stu-id="f58be-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="f58be-119">Se il documento di Swagger non soddisfa questo requisito, è possibile usare [Archiviazione di Azure con CORS abilitato](#hosting-swagger-from-storage) per archiviare il documento.</span><span class="sxs-lookup"><span data-stu-id="f58be-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="f58be-120">Fare clic su **Avanti** per leggere e visualizzare il documento di Swagger.</span><span class="sxs-lookup"><span data-stu-id="f58be-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="f58be-121">Aggiungere i parametri richiesti per la chiamata HTTP.</span><span class="sxs-lookup"><span data-stu-id="f58be-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Completare l'azione HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="f58be-123">Per salvare e pubblicare un'app per la logica, fare clic su **Salva** nella barra degli strumenti della finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="f58be-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="f58be-124">Ospitare Swagger da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f58be-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="f58be-125">Si consiglia di fare riferimento a un documento di Swagger che non sia ospitato o non soddisfi i requisiti di sicurezza e origini multiple per la finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="f58be-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="f58be-126">Per risolvere questo problema, è possibile archiviare il documento di Swagger in Archiviazione di Azure e abilitare CORS a fare riferimento al documento.</span><span class="sxs-lookup"><span data-stu-id="f58be-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="f58be-127">Ecco i passaggi per creare, configurare e archiviare i documenti di Swagger in Archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="f58be-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="f58be-128">[Creare un account di Archiviazione di Azure con Archiviazione BLOB di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f58be-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="f58be-129">Per eseguire questo passaggio, impostare le autorizzazioni su **Accesso pubblico**.</span><span class="sxs-lookup"><span data-stu-id="f58be-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="f58be-130">Abilitare CORS nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="f58be-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="f58be-131">Per configurare tale impostazione automaticamente è possibile usare [questo script di PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="f58be-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="f58be-132">Caricare il file di Swagger nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="f58be-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="f58be-133">È possibile eseguire questo passaggio nel [portale di Azure](https://portal.azure.com) o con uno strumento come [Esplora archivi di Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f58be-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="f58be-134">Rimandare un collegamento HTTPS al documento nell'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="f58be-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="f58be-135">Il collegamento usa questo formato:</span><span class="sxs-lookup"><span data-stu-id="f58be-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="f58be-136">Dettagli tecnici</span><span class="sxs-lookup"><span data-stu-id="f58be-136">Technical details</span></span>
<span data-ttu-id="f58be-137">Di seguito sono riportati i dettagli per i trigger e le azioni supportati da questo connettore HTTP + Swagger.</span><span class="sxs-lookup"><span data-stu-id="f58be-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="f58be-138">Trigger HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="f58be-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="f58be-139">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f58be-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="f58be-140">Altre informazioni sui trigger.</span><span class="sxs-lookup"><span data-stu-id="f58be-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="f58be-141">Il connettore HTTP + Swagger supporta un solo trigger.</span><span class="sxs-lookup"><span data-stu-id="f58be-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="f58be-142">Trigger</span><span class="sxs-lookup"><span data-stu-id="f58be-142">Trigger</span></span> | <span data-ttu-id="f58be-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f58be-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f58be-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="f58be-144">HTTP + Swagger</span></span> |<span data-ttu-id="f58be-145">Esegue una chiamata HTTP e restituisce il contenuto della risposta</span><span class="sxs-lookup"><span data-stu-id="f58be-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="f58be-146">Azioni HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="f58be-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="f58be-147">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f58be-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="f58be-148">Ulteriori informazioni sulle azioni.</span><span class="sxs-lookup"><span data-stu-id="f58be-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="f58be-149">Il connettore HTTP + Swagger supporta una sola azione possibile.</span><span class="sxs-lookup"><span data-stu-id="f58be-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="f58be-150">Azione</span><span class="sxs-lookup"><span data-stu-id="f58be-150">Action</span></span> | <span data-ttu-id="f58be-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f58be-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f58be-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="f58be-152">HTTP + Swagger</span></span> |<span data-ttu-id="f58be-153">Esegue una chiamata HTTP e restituisce il contenuto della risposta</span><span class="sxs-lookup"><span data-stu-id="f58be-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="f58be-154">Informazioni dettagliate sulle azioni</span><span class="sxs-lookup"><span data-stu-id="f58be-154">Action details</span></span>
<span data-ttu-id="f58be-155">Il connettore HTTP + Swagger include una sola azione possibile.</span><span class="sxs-lookup"><span data-stu-id="f58be-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="f58be-156">Di seguito sono riportate le informazioni su ognuna delle azioni, i relativi campi di input obbligatori e facoltativi e i corrispondenti dettagli di output associati al loro uso.</span><span class="sxs-lookup"><span data-stu-id="f58be-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="f58be-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="f58be-157">HTTP + Swagger</span></span>
<span data-ttu-id="f58be-158">Eseguire una richiesta HTTP in uscita con l'assistenza dei metadati Swagger.</span><span class="sxs-lookup"><span data-stu-id="f58be-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="f58be-159">L'asterisco (*) indica un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f58be-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="f58be-160">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="f58be-160">Display name</span></span> | <span data-ttu-id="f58be-161">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="f58be-161">Property name</span></span> | <span data-ttu-id="f58be-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f58be-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f58be-163">Metodo*</span><span class="sxs-lookup"><span data-stu-id="f58be-163">Method*</span></span> |<span data-ttu-id="f58be-164">statico</span><span class="sxs-lookup"><span data-stu-id="f58be-164">method</span></span> |<span data-ttu-id="f58be-165">Verbo HTTP da usare.</span><span class="sxs-lookup"><span data-stu-id="f58be-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="f58be-166">URI*</span><span class="sxs-lookup"><span data-stu-id="f58be-166">URI*</span></span> |<span data-ttu-id="f58be-167">Uri</span><span class="sxs-lookup"><span data-stu-id="f58be-167">uri</span></span> |<span data-ttu-id="f58be-168">URI per la richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="f58be-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="f58be-169">Headers</span><span class="sxs-lookup"><span data-stu-id="f58be-169">Headers</span></span> |<span data-ttu-id="f58be-170">Headers</span><span class="sxs-lookup"><span data-stu-id="f58be-170">headers</span></span> |<span data-ttu-id="f58be-171">Un oggetto JSON delle intestazioni HTTP da includere.</span><span class="sxs-lookup"><span data-stu-id="f58be-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="f58be-172">Corpo</span><span class="sxs-lookup"><span data-stu-id="f58be-172">Body</span></span> |<span data-ttu-id="f58be-173">Corpo</span><span class="sxs-lookup"><span data-stu-id="f58be-173">body</span></span> |<span data-ttu-id="f58be-174">Il corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="f58be-174">The HTTP request body.</span></span> |
| <span data-ttu-id="f58be-175">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="f58be-175">Authentication</span></span> |<span data-ttu-id="f58be-176">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="f58be-176">authentication</span></span> |<span data-ttu-id="f58be-177">Autenticazione da usare per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="f58be-177">Authentication to use for request.</span></span> <span data-ttu-id="f58be-178">Per altre informazioni, vedere il [connettore HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="f58be-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="f58be-179">**Dettagli dell'output**</span><span class="sxs-lookup"><span data-stu-id="f58be-179">**Output details**</span></span>

<span data-ttu-id="f58be-180">Risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="f58be-180">HTTP response</span></span>

| <span data-ttu-id="f58be-181">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="f58be-181">Property Name</span></span> | <span data-ttu-id="f58be-182">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="f58be-182">Data type</span></span> | <span data-ttu-id="f58be-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f58be-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f58be-184">headers</span><span class="sxs-lookup"><span data-stu-id="f58be-184">Headers</span></span> |<span data-ttu-id="f58be-185">object</span><span class="sxs-lookup"><span data-stu-id="f58be-185">object</span></span> |<span data-ttu-id="f58be-186">Intestazioni della risposta</span><span class="sxs-lookup"><span data-stu-id="f58be-186">Response headers</span></span> |
| <span data-ttu-id="f58be-187">Corpo</span><span class="sxs-lookup"><span data-stu-id="f58be-187">Body</span></span> |<span data-ttu-id="f58be-188">object</span><span class="sxs-lookup"><span data-stu-id="f58be-188">object</span></span> |<span data-ttu-id="f58be-189">Oggetto della risposta</span><span class="sxs-lookup"><span data-stu-id="f58be-189">Response object</span></span> |
| <span data-ttu-id="f58be-190">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="f58be-190">Status Code</span></span> |<span data-ttu-id="f58be-191">int</span><span class="sxs-lookup"><span data-stu-id="f58be-191">int</span></span> |<span data-ttu-id="f58be-192">Stato codice HTTP</span><span class="sxs-lookup"><span data-stu-id="f58be-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="f58be-193">Risposte HTTP</span><span class="sxs-lookup"><span data-stu-id="f58be-193">HTTP responses</span></span>
<span data-ttu-id="f58be-194">Quando si eseguono chiamate a varie azioni, è possibile ottenere determinate risposte.</span><span class="sxs-lookup"><span data-stu-id="f58be-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="f58be-195">Di seguito è riportata una tabella contenente le risposte e le descrizioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="f58be-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="f58be-196">Nome</span><span class="sxs-lookup"><span data-stu-id="f58be-196">Name</span></span> | <span data-ttu-id="f58be-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f58be-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f58be-198">200</span><span class="sxs-lookup"><span data-stu-id="f58be-198">200</span></span> |<span data-ttu-id="f58be-199">OK</span><span class="sxs-lookup"><span data-stu-id="f58be-199">OK</span></span> |
| <span data-ttu-id="f58be-200">202</span><span class="sxs-lookup"><span data-stu-id="f58be-200">202</span></span> |<span data-ttu-id="f58be-201">Accepted</span><span class="sxs-lookup"><span data-stu-id="f58be-201">Accepted</span></span> |
| <span data-ttu-id="f58be-202">400</span><span class="sxs-lookup"><span data-stu-id="f58be-202">400</span></span> |<span data-ttu-id="f58be-203">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="f58be-203">Bad request</span></span> |
| <span data-ttu-id="f58be-204">401</span><span class="sxs-lookup"><span data-stu-id="f58be-204">401</span></span> |<span data-ttu-id="f58be-205">Non autorizzata</span><span class="sxs-lookup"><span data-stu-id="f58be-205">Unauthorized</span></span> |
| <span data-ttu-id="f58be-206">403</span><span class="sxs-lookup"><span data-stu-id="f58be-206">403</span></span> |<span data-ttu-id="f58be-207">Accesso negato</span><span class="sxs-lookup"><span data-stu-id="f58be-207">Forbidden</span></span> |
| <span data-ttu-id="f58be-208">404</span><span class="sxs-lookup"><span data-stu-id="f58be-208">404</span></span> |<span data-ttu-id="f58be-209">Non trovato</span><span class="sxs-lookup"><span data-stu-id="f58be-209">Not Found</span></span> |
| <span data-ttu-id="f58be-210">500</span><span class="sxs-lookup"><span data-stu-id="f58be-210">500</span></span> |<span data-ttu-id="f58be-211">Errore interno del server.</span><span class="sxs-lookup"><span data-stu-id="f58be-211">Internal server error.</span></span> <span data-ttu-id="f58be-212">Si è verificato un errore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="f58be-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="f58be-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f58be-213">Next steps</span></span>

* [<span data-ttu-id="f58be-214">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f58be-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="f58be-215">Trovare altri connettori</span><span class="sxs-lookup"><span data-stu-id="f58be-215">Find other connectors</span></span>](apis-list.md)