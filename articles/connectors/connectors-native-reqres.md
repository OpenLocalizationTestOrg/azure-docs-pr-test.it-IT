---
title: Usare le azioni di richiesta e risposta | Documentazione Microsoft
description: Panoramica del trigger e dell'azione di richiesta e risposta in un'app per la logica di Azure
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="4cfe4-103">Introduzione ai componenti di richiesta e risposta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-103">Get started with the request and response components</span></span>
<span data-ttu-id="4cfe4-104">Con i componenti di richiesta e risposta in un'app per la logica è possibile rispondere in tempo reale agli eventi.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="4cfe4-105">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="4cfe4-105">For example, you can:</span></span>

* <span data-ttu-id="4cfe4-106">Rispondere a una richiesta HTTP con i dati di un database locale tramite un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="4cfe4-107">Attivare un'app per la logica da un evento webhook esterno.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="4cfe4-108">Chiamare un'app per la logica con un'azione di richiesta e risposta dall'interno di un'altra app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="4cfe4-109">Per informazioni su come iniziare a usare le azioni di richiesta e risposta in un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4cfe4-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="4cfe4-110">Usare il trigger di richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="4cfe4-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="4cfe4-111">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="4cfe4-112">[Altre informazioni sui trigger](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4cfe4-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="4cfe4-113">Ecco una sequenza di esempio di come configurare una richiesta HTTP nella finestra di progettazione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="4cfe4-114">Aggiungere il trigger **Richiesta - Alla ricezione di una richiesta HTTP** all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="4cfe4-115">È possibile facoltativamente fornire uno schema JSON (usando uno strumento come [JSONSchema.net](http://jsonschema.net)) per il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="4cfe4-116">In questo modo la finestra di progettazione potrà generare i token per le proprietà nella richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="4cfe4-117">Aggiungere un'altra azione per poter salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="4cfe4-118">Dopo il salvataggio dell'app per la logica, è possibile ottenere l'URL della richiesta HTTP dalla scheda di richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="4cfe4-119">Un HTTP POST (è possibile usare uno strumento come [Postman](https://www.getpostman.com/)) all'URL attiva l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="4cfe4-120">Se non viene definita un'azione di risposta, una risposta `202 ACCEPTED` viene restituita immediatamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="4cfe4-121">È possibile usare l'azione di risposta per personalizzare una risposta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-121">You can use the response action to customize a response.</span></span>
> 
> 

![Trigger di risposta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="4cfe4-123">Usare l'azione di risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="4cfe4-123">Use the HTTP Response action</span></span>
<span data-ttu-id="4cfe4-124">L'azione di risposta HTTP è valida solo quando viene usata in un flusso di lavoro attivato da una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="4cfe4-125">Se non viene definita un'azione di risposta, una risposta `202 ACCEPTED` viene restituita immediatamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="4cfe4-126">È possibile aggiungere un'azione di risposta in qualsiasi passaggio nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="4cfe4-127">L'app per la logica mantiene aperta la richiesta in ingresso per una risposta solo per un minuto.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="4cfe4-128">Dopo un minuto, se non è stata inviata alcuna risposta dal flusso di lavoro (e nella definizione è presente un'azione di risposta), viene restituito un `504 GATEWAY TIMEOUT` al chiamante.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="4cfe4-129">Ecco come aggiungere un'azione di risposta HTTP:</span><span class="sxs-lookup"><span data-stu-id="4cfe4-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="4cfe4-130">Fare clic sul pulsante **Nuovo passaggio** .</span><span class="sxs-lookup"><span data-stu-id="4cfe4-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="4cfe4-131">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="4cfe4-132">Nella casella di ricerca azione digitare **response** per elencare l'azione di risposta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Selezionare l'azione di risposta](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="4cfe4-134">Aggiungere i parametri richiesti per il messaggio di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![Completare l'azione di risposta](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="4cfe4-136">Fare clic sull'angolo in alto a sinistra della barra degli strumenti per salvare e pubblicare (attivare) l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="4cfe4-137">Trigger di richiesta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-137">Request trigger</span></span>
<span data-ttu-id="4cfe4-138">Ecco i dettagli per il trigger supportato da questo connettore.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="4cfe4-139">È disponibile un solo trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-139">There is a single request trigger.</span></span>

| <span data-ttu-id="4cfe4-140">Trigger</span><span class="sxs-lookup"><span data-stu-id="4cfe4-140">Trigger</span></span> | <span data-ttu-id="4cfe4-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cfe4-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4cfe4-142">Richiesta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-142">Request</span></span> |<span data-ttu-id="4cfe4-143">Si verifica quando viene ricevuta una richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="4cfe4-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="4cfe4-144">Azione di risposta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-144">Response action</span></span>
<span data-ttu-id="4cfe4-145">Ecco i dettagli per l'azione supportata da questo connettore.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="4cfe4-146">Esiste una sola azione di risposta che può essere usata solo quando è accompagnata da un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="4cfe4-147">Azione</span><span class="sxs-lookup"><span data-stu-id="4cfe4-147">Action</span></span> | <span data-ttu-id="4cfe4-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cfe4-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4cfe4-149">response</span><span class="sxs-lookup"><span data-stu-id="4cfe4-149">Response</span></span> |<span data-ttu-id="4cfe4-150">Restituisce una risposta alla richiesta HTTP correlata</span><span class="sxs-lookup"><span data-stu-id="4cfe4-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="4cfe4-151">Dettagli sui trigger e le azioni</span><span class="sxs-lookup"><span data-stu-id="4cfe4-151">Trigger and action details</span></span>
<span data-ttu-id="4cfe4-152">Le tabelle seguenti descrivono i campi di input per il trigger e l'azione e i corrispondenti dettagli di output.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="4cfe4-153">Trigger di richiesta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-153">Request trigger</span></span>
<span data-ttu-id="4cfe4-154">Di seguito è riportato un campo di input per il trigger da una richiesta HTTP in ingresso.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="4cfe4-155">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="4cfe4-155">Display name</span></span> | <span data-ttu-id="4cfe4-156">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="4cfe4-156">Property name</span></span> | <span data-ttu-id="4cfe4-157">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cfe4-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cfe4-158">Schema JSON</span><span class="sxs-lookup"><span data-stu-id="4cfe4-158">JSON Schema</span></span> |<span data-ttu-id="4cfe4-159">schema</span><span class="sxs-lookup"><span data-stu-id="4cfe4-159">schema</span></span> |<span data-ttu-id="4cfe4-160">Lo schema JSON del corpo della richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="4cfe4-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="4cfe4-161">**Dettagli dell'output**</span><span class="sxs-lookup"><span data-stu-id="4cfe4-161">**Output details**</span></span>

<span data-ttu-id="4cfe4-162">Di seguito sono indicati i dettagli di output per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-162">The following are output details for the request.</span></span>

| <span data-ttu-id="4cfe4-163">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="4cfe4-163">Property name</span></span> | <span data-ttu-id="4cfe4-164">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="4cfe4-164">Data type</span></span> | <span data-ttu-id="4cfe4-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cfe4-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cfe4-166">headers</span><span class="sxs-lookup"><span data-stu-id="4cfe4-166">Headers</span></span> |<span data-ttu-id="4cfe4-167">object</span><span class="sxs-lookup"><span data-stu-id="4cfe4-167">object</span></span> |<span data-ttu-id="4cfe4-168">Intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-168">Request headers</span></span> |
| <span data-ttu-id="4cfe4-169">Corpo</span><span class="sxs-lookup"><span data-stu-id="4cfe4-169">Body</span></span> |<span data-ttu-id="4cfe4-170">object</span><span class="sxs-lookup"><span data-stu-id="4cfe4-170">object</span></span> |<span data-ttu-id="4cfe4-171">Oggetto della richiesta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="4cfe4-172">Azione di risposta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-172">Response action</span></span>
<span data-ttu-id="4cfe4-173">Di seguito sono riportati i campi di input per l'azione di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="4cfe4-174">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="4cfe4-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="4cfe4-175">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="4cfe4-175">Display name</span></span> | <span data-ttu-id="4cfe4-176">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="4cfe4-176">Property name</span></span> | <span data-ttu-id="4cfe4-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cfe4-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4cfe4-178">Codice di stato*</span><span class="sxs-lookup"><span data-stu-id="4cfe4-178">Status Code*</span></span> |<span data-ttu-id="4cfe4-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="4cfe4-179">statusCode</span></span> |<span data-ttu-id="4cfe4-180">Il codice di stato HTTP</span><span class="sxs-lookup"><span data-stu-id="4cfe4-180">The HTTP status code</span></span> |
| <span data-ttu-id="4cfe4-181">Headers</span><span class="sxs-lookup"><span data-stu-id="4cfe4-181">Headers</span></span> |<span data-ttu-id="4cfe4-182">Headers</span><span class="sxs-lookup"><span data-stu-id="4cfe4-182">headers</span></span> |<span data-ttu-id="4cfe4-183">Un oggetto JSON delle intestazioni HTTP da includere</span><span class="sxs-lookup"><span data-stu-id="4cfe4-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="4cfe4-184">Corpo</span><span class="sxs-lookup"><span data-stu-id="4cfe4-184">Body</span></span> |<span data-ttu-id="4cfe4-185">Corpo</span><span class="sxs-lookup"><span data-stu-id="4cfe4-185">body</span></span> |<span data-ttu-id="4cfe4-186">Il corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="4cfe4-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4cfe4-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cfe4-187">Next steps</span></span>
<span data-ttu-id="4cfe4-188">Provare ora a usare la piattaforma e [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4cfe4-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4cfe4-189">È possibile esplorare gli altri connettori disponibili nelle app per la logica esaminando l' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4cfe4-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

