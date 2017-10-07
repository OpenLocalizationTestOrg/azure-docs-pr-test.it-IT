---
title: azioni di richiesta e risposta aaaUse | Documenti Microsoft
description: Panoramica di trigger di richiesta e risposta hello e azione in un'applicazione Azure logica
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="8ee3a-103">Iniziare con i componenti di richiesta e risposta hello</span><span class="sxs-lookup"><span data-stu-id="8ee3a-103">Get started with hello request and response components</span></span>
<span data-ttu-id="8ee3a-104">Con hello richiesta e risposta componenti in un'app di logica, è possibile rispondere in tempo reale tooevents.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="8ee3a-105">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="8ee3a-105">For example, you can:</span></span>

* <span data-ttu-id="8ee3a-106">Rispondere tooan di richiesta HTTP con i dati da un database locale tramite un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="8ee3a-107">Attivare un'app per la logica da un evento webhook esterno.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="8ee3a-108">Chiamare un'app per la logica con un'azione di richiesta e risposta dall'interno di un'altra app per la logica.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="8ee3a-109">tooget avviate tramite operazioni di richiesta e risposta hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8ee3a-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="8ee3a-110">Utilizzare trigger di richiesta HTTP hello</span><span class="sxs-lookup"><span data-stu-id="8ee3a-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="8ee3a-111">Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="8ee3a-112">[Altre informazioni sui trigger](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ee3a-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="8ee3a-113">Di seguito è riportata una sequenza di esempio di come tooset backup HTTP richiesta in Progettazione applicazione logica hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="8ee3a-114">Aggiungere trigger hello **richiesta - viene ricevuta la richiesta HTTP quando** nell'app logica.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="8ee3a-115">È anche possibile specificare uno schema JSON (utilizzando uno strumento come [JSONSchema.net](http://jsonschema.net)) per il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="8ee3a-116">In questo modo i token della finestra di progettazione toogenerate hello per le proprietà nella richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="8ee3a-117">Aggiungere un'altra operazione in modo che sia possibile salvare hello logica app.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="8ee3a-118">Dopo aver salvato hello logica app, è possibile ottenere l'URL della richiesta HTTP hello dalla scheda richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="8ee3a-119">Un POST HTTP (è possibile utilizzare uno strumento come [Postman](https://www.getpostman.com/)) trigger URL toohello hello logica app.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="8ee3a-120">Se non si definisce un'azione di risposta, un `202 ACCEPTED` risposta viene restituita immediatamente toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="8ee3a-121">È possibile utilizzare hello risposta azione toocustomize una risposta.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Trigger di risposta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="8ee3a-123">Utilizzare l'azione di risposta HTTP hello</span><span class="sxs-lookup"><span data-stu-id="8ee3a-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="8ee3a-124">azione di risposta HTTP Hello è valida solo quando si usa un flusso di lavoro attivato da una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="8ee3a-125">Se non si definisce un'azione di risposta, un `202 ACCEPTED` risposta viene restituita immediatamente toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="8ee3a-126">È possibile aggiungere un'azione di risposta in un passaggio all'interno del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="8ee3a-127">app per la logica Hello mantiene solo aperta richiesta in ingresso hello per un minuto per una risposta.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="8ee3a-128">Dopo un minuto, se è stata inviata alcuna risposta dal flusso di lavoro hello (e un'azione di risposta è presente nella definizione di hello), un `504 GATEWAY TIMEOUT` viene restituito toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="8ee3a-129">Ecco come tooadd un'azione di risposta HTTP:</span><span class="sxs-lookup"><span data-stu-id="8ee3a-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="8ee3a-130">Seleziona hello **nuovo passaggio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="8ee3a-131">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="8ee3a-132">Nella casella di ricerca azione hello, digitare **risposta** hello toolist azione di risposta.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Selezionare l'azione di risposta hello](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="8ee3a-134">Aggiungere i parametri necessari per il messaggio di risposta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Azione di risposta hello completo](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="8ee3a-136">Fare clic su nell'angolo superiore sinistro hello di hello barra degli strumenti toosave e la logica app verrà entrambi salvare e pubblicare (attivare).</span><span class="sxs-lookup"><span data-stu-id="8ee3a-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="8ee3a-137">Trigger di richiesta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-137">Request trigger</span></span>
<span data-ttu-id="8ee3a-138">Ecco i dettagli di hello per trigger hello che supporta il connettore.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="8ee3a-139">È disponibile un solo trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-139">There is a single request trigger.</span></span>

| <span data-ttu-id="8ee3a-140">Trigger</span><span class="sxs-lookup"><span data-stu-id="8ee3a-140">Trigger</span></span> | <span data-ttu-id="8ee3a-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ee3a-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ee3a-142">Richiesta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-142">Request</span></span> |<span data-ttu-id="8ee3a-143">Si verifica quando viene ricevuta una richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8ee3a-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="8ee3a-144">Azione di risposta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-144">Response action</span></span>
<span data-ttu-id="8ee3a-145">Ecco hello dettagli per l'azione di hello che supporta questo connettore.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="8ee3a-146">Esiste una sola azione di risposta che può essere usata solo quando è accompagnata da un trigger di richiesta.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="8ee3a-147">Azione</span><span class="sxs-lookup"><span data-stu-id="8ee3a-147">Action</span></span> | <span data-ttu-id="8ee3a-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ee3a-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ee3a-149">Response</span><span class="sxs-lookup"><span data-stu-id="8ee3a-149">Response</span></span> |<span data-ttu-id="8ee3a-150">Restituisce che una risposta toohello correlati richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8ee3a-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="8ee3a-151">Dettagli sui trigger e le azioni</span><span class="sxs-lookup"><span data-stu-id="8ee3a-151">Trigger and action details</span></span>
<span data-ttu-id="8ee3a-152">Hello nelle tabelle seguenti vengono descritti i campi di input hello per trigger hello e l'azione e hello dettagli output corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="8ee3a-153">Trigger di richiesta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-153">Request trigger</span></span>
<span data-ttu-id="8ee3a-154">di seguito Hello è un campo di input per il trigger hello da una richiesta HTTP in ingresso.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="8ee3a-155">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="8ee3a-155">Display name</span></span> | <span data-ttu-id="8ee3a-156">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="8ee3a-156">Property name</span></span> | <span data-ttu-id="8ee3a-157">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ee3a-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ee3a-158">Schema JSON</span><span class="sxs-lookup"><span data-stu-id="8ee3a-158">JSON Schema</span></span> |<span data-ttu-id="8ee3a-159">schema</span><span class="sxs-lookup"><span data-stu-id="8ee3a-159">schema</span></span> |<span data-ttu-id="8ee3a-160">schema JSON Hello del corpo della richiesta HTTP hello</span><span class="sxs-lookup"><span data-stu-id="8ee3a-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="8ee3a-161">**Dettagli dell'output**</span><span class="sxs-lookup"><span data-stu-id="8ee3a-161">**Output details**</span></span>

<span data-ttu-id="8ee3a-162">di seguito Hello sono i dettagli di output per la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="8ee3a-163">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="8ee3a-163">Property name</span></span> | <span data-ttu-id="8ee3a-164">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="8ee3a-164">Data type</span></span> | <span data-ttu-id="8ee3a-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ee3a-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ee3a-166">headers</span><span class="sxs-lookup"><span data-stu-id="8ee3a-166">Headers</span></span> |<span data-ttu-id="8ee3a-167">object</span><span class="sxs-lookup"><span data-stu-id="8ee3a-167">object</span></span> |<span data-ttu-id="8ee3a-168">Intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-168">Request headers</span></span> |
| <span data-ttu-id="8ee3a-169">Corpo</span><span class="sxs-lookup"><span data-stu-id="8ee3a-169">Body</span></span> |<span data-ttu-id="8ee3a-170">object</span><span class="sxs-lookup"><span data-stu-id="8ee3a-170">object</span></span> |<span data-ttu-id="8ee3a-171">Oggetto della richiesta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="8ee3a-172">Azione di risposta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-172">Response action</span></span>
<span data-ttu-id="8ee3a-173">di seguito Hello sono campi di input per hello azione di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="8ee3a-174">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="8ee3a-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="8ee3a-175">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="8ee3a-175">Display name</span></span> | <span data-ttu-id="8ee3a-176">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="8ee3a-176">Property name</span></span> | <span data-ttu-id="8ee3a-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ee3a-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ee3a-178">Codice di stato*</span><span class="sxs-lookup"><span data-stu-id="8ee3a-178">Status Code*</span></span> |<span data-ttu-id="8ee3a-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="8ee3a-179">statusCode</span></span> |<span data-ttu-id="8ee3a-180">codice di stato HTTP Hello</span><span class="sxs-lookup"><span data-stu-id="8ee3a-180">hello HTTP status code</span></span> |
| <span data-ttu-id="8ee3a-181">Headers</span><span class="sxs-lookup"><span data-stu-id="8ee3a-181">Headers</span></span> |<span data-ttu-id="8ee3a-182">headers</span><span class="sxs-lookup"><span data-stu-id="8ee3a-182">headers</span></span> |<span data-ttu-id="8ee3a-183">Un oggetto JSON di qualsiasi tooinclude di intestazioni di risposta</span><span class="sxs-lookup"><span data-stu-id="8ee3a-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="8ee3a-184">Corpo</span><span class="sxs-lookup"><span data-stu-id="8ee3a-184">Body</span></span> |<span data-ttu-id="8ee3a-185">body</span><span class="sxs-lookup"><span data-stu-id="8ee3a-185">body</span></span> |<span data-ttu-id="8ee3a-186">corpo della risposta Hello</span><span class="sxs-lookup"><span data-stu-id="8ee3a-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ee3a-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ee3a-187">Next steps</span></span>
<span data-ttu-id="8ee3a-188">A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8ee3a-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="8ee3a-189">È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8ee3a-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

