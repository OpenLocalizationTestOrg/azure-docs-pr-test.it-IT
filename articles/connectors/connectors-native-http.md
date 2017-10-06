---
title: aaaCommunicate con qualsiasi endpoint su HTTP, le app di logica di Azure | Documenti Microsoft
description: Creare app per la logica in grado di comunicare con qualsiasi endpoint su HTTP
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="05bb2-103">Introduzione a hello azione HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="05bb2-104">Con hello azione HTTP, è possibile estendere i flussi di lavoro per l'organizzazione e comunicare tooany endpoint su HTTP.</span><span class="sxs-lookup"><span data-stu-id="05bb2-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="05bb2-105">È possibile:</span><span class="sxs-lookup"><span data-stu-id="05bb2-105">You can:</span></span>

* <span data-ttu-id="05bb2-106">Creare flussi di lavoro con app per la logica che si attivano (trigger) quando un sito Web gestito diventa inattivo.</span><span class="sxs-lookup"><span data-stu-id="05bb2-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="05bb2-107">Comunicare tooany endpoint tramite HTTP tooextend i flussi di lavoro ad altri servizi.</span><span class="sxs-lookup"><span data-stu-id="05bb2-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="05bb2-108">tooget avviato utilizzando l'azione di hello HTTP in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="05bb2-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="05bb2-109">Utilizzare trigger hello HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="05bb2-110">Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="05bb2-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="05bb2-111">[Altre informazioni sui trigger](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05bb2-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="05bb2-112">Di seguito è riportata una sequenza di esempio di come trigger tooset backup hello HTTP hello progettazione applicazione logica.</span><span class="sxs-lookup"><span data-stu-id="05bb2-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="05bb2-113">Aggiungere trigger di hello HTTP nell'app logica.</span><span class="sxs-lookup"><span data-stu-id="05bb2-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="05bb2-114">Specificare i parametri di hello per endpoint hello HTTP che si desidera toopoll.</span><span class="sxs-lookup"><span data-stu-id="05bb2-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="05bb2-115">Modificare l'intervallo di ricorrenza hello sulla frequenza con cui deve eseguire il polling.</span><span class="sxs-lookup"><span data-stu-id="05bb2-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="05bb2-116">Hello logica app viene ora attivato con il contenuto restituito durante ogni controllo.</span><span class="sxs-lookup"><span data-stu-id="05bb2-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Trigger HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="05bb2-118">Funzionamento di trigger HTTP hello</span><span class="sxs-lookup"><span data-stu-id="05bb2-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="05bb2-119">trigger di Hello HTTP invia un endpoint tooHTTP chiamata su un intervallo di ricorrenza.</span><span class="sxs-lookup"><span data-stu-id="05bb2-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="05bb2-120">Per impostazione predefinita, il codice di risposta HTTP che è inferiore a 300 provoca un toorun app logica.</span><span class="sxs-lookup"><span data-stu-id="05bb2-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="05bb2-121">toospecify se deve generare hello logica app, è possibile modificare hello logica app nella visualizzazione codice e aggiungere una condizione che restituisce hello dopo la chiamata HTTP.</span><span class="sxs-lookup"><span data-stu-id="05bb2-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="05bb2-122">Di seguito è riportato un esempio di un trigger HTTP che viene generato quando hello restituito codice di stato è maggiore o uguale a troppo`400`.</span><span class="sxs-lookup"><span data-stu-id="05bb2-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="05bb2-123">Per maggiori informazioni sui parametri trigger hello HTTP, disponibile in [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="05bb2-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="05bb2-124">Utilizzare l'azione di hello HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-124">Use hello HTTP action</span></span>

<span data-ttu-id="05bb2-125">Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="05bb2-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="05bb2-126">[Altre informazioni sulle azioni](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05bb2-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="05bb2-127">Scegliere **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="05bb2-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="05bb2-128">Nella casella di ricerca azione hello, digitare **http** azioni hello HTTP toolist.</span><span class="sxs-lookup"><span data-stu-id="05bb2-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Selezionare l'azione di hello HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="05bb2-130">Aggiungere i parametri richiesti per la chiamata hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="05bb2-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Hello completo azione HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="05bb2-132">Sulla barra degli strumenti della finestra di progettazione hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="05bb2-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="05bb2-133">L'app logica viene salvato e pubblicato (attivato) hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="05bb2-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="05bb2-134">Trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-134">HTTP trigger</span></span>
<span data-ttu-id="05bb2-135">Ecco i dettagli di hello per trigger hello che supporta il connettore.</span><span class="sxs-lookup"><span data-stu-id="05bb2-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="05bb2-136">Connettore HTTP Hello include un trigger.</span><span class="sxs-lookup"><span data-stu-id="05bb2-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="05bb2-137">Trigger</span><span class="sxs-lookup"><span data-stu-id="05bb2-137">Trigger</span></span> | <span data-ttu-id="05bb2-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05bb2-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-139">HTTP</span></span> |<span data-ttu-id="05bb2-140">Effettua una chiamata HTTP e restituisce contenuto della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="05bb2-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="05bb2-141">Azione HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-141">HTTP action</span></span>
<span data-ttu-id="05bb2-142">Ecco hello dettagli per l'azione di hello che supporta questo connettore.</span><span class="sxs-lookup"><span data-stu-id="05bb2-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="05bb2-143">Connettore HTTP Hello è un'opzione possibile.</span><span class="sxs-lookup"><span data-stu-id="05bb2-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="05bb2-144">Azione</span><span class="sxs-lookup"><span data-stu-id="05bb2-144">Action</span></span> | <span data-ttu-id="05bb2-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05bb2-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-146">HTTP</span></span> |<span data-ttu-id="05bb2-147">Effettua una chiamata HTTP e restituisce contenuto della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="05bb2-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="05bb2-148">Dettagli di HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-148">HTTP details</span></span>
<span data-ttu-id="05bb2-149">Hello nelle tabelle seguenti vengono descritti hello necessarie e i campi di input facoltativi per azione di hello e i dettagli di output corrispondenti hello associati mediante l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="05bb2-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="05bb2-150">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-150">HTTP request</span></span>
<span data-ttu-id="05bb2-151">di seguito Hello sono campi di input per l'azione di hello, che esegue una richiesta HTTP in uscita.</span><span class="sxs-lookup"><span data-stu-id="05bb2-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="05bb2-152">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="05bb2-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="05bb2-153">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="05bb2-153">Display name</span></span> | <span data-ttu-id="05bb2-154">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="05bb2-154">Property name</span></span> | <span data-ttu-id="05bb2-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05bb2-156">Metodo*</span><span class="sxs-lookup"><span data-stu-id="05bb2-156">Method*</span></span> |<span data-ttu-id="05bb2-157">statico</span><span class="sxs-lookup"><span data-stu-id="05bb2-157">method</span></span> |<span data-ttu-id="05bb2-158">toouse verbo HTTP Hello</span><span class="sxs-lookup"><span data-stu-id="05bb2-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="05bb2-159">URI*</span><span class="sxs-lookup"><span data-stu-id="05bb2-159">URI*</span></span> |<span data-ttu-id="05bb2-160">Uri</span><span class="sxs-lookup"><span data-stu-id="05bb2-160">uri</span></span> |<span data-ttu-id="05bb2-161">Hello URI per la richiesta HTTP hello</span><span class="sxs-lookup"><span data-stu-id="05bb2-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="05bb2-162">Headers</span><span class="sxs-lookup"><span data-stu-id="05bb2-162">Headers</span></span> |<span data-ttu-id="05bb2-163">headers</span><span class="sxs-lookup"><span data-stu-id="05bb2-163">headers</span></span> |<span data-ttu-id="05bb2-164">Un oggetto JSON di tooinclude intestazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="05bb2-165">Corpo</span><span class="sxs-lookup"><span data-stu-id="05bb2-165">Body</span></span> |<span data-ttu-id="05bb2-166">body</span><span class="sxs-lookup"><span data-stu-id="05bb2-166">body</span></span> |<span data-ttu-id="05bb2-167">Hello corpo della richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-167">hello HTTP request body</span></span> |
| <span data-ttu-id="05bb2-168">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="05bb2-168">Authentication</span></span> |<span data-ttu-id="05bb2-169">authentication</span><span class="sxs-lookup"><span data-stu-id="05bb2-169">authentication</span></span> |<span data-ttu-id="05bb2-170">Dettagli hello [autenticazione](#authentication) sezione</span><span class="sxs-lookup"><span data-stu-id="05bb2-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="05bb2-171">Dettagli dell'output</span><span class="sxs-lookup"><span data-stu-id="05bb2-171">Output details</span></span>
<span data-ttu-id="05bb2-172">di seguito Hello sono i dettagli di output per hello risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="05bb2-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="05bb2-173">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="05bb2-173">Property name</span></span> | <span data-ttu-id="05bb2-174">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="05bb2-174">Data type</span></span> | <span data-ttu-id="05bb2-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05bb2-176">headers</span><span class="sxs-lookup"><span data-stu-id="05bb2-176">Headers</span></span> |<span data-ttu-id="05bb2-177">object</span><span class="sxs-lookup"><span data-stu-id="05bb2-177">object</span></span> |<span data-ttu-id="05bb2-178">Intestazioni della risposta</span><span class="sxs-lookup"><span data-stu-id="05bb2-178">Response headers</span></span> |
| <span data-ttu-id="05bb2-179">Corpo</span><span class="sxs-lookup"><span data-stu-id="05bb2-179">Body</span></span> |<span data-ttu-id="05bb2-180">object</span><span class="sxs-lookup"><span data-stu-id="05bb2-180">object</span></span> |<span data-ttu-id="05bb2-181">Oggetto della risposta</span><span class="sxs-lookup"><span data-stu-id="05bb2-181">Response object</span></span> |
| <span data-ttu-id="05bb2-182">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="05bb2-182">Status Code</span></span> |<span data-ttu-id="05bb2-183">int</span><span class="sxs-lookup"><span data-stu-id="05bb2-183">int</span></span> |<span data-ttu-id="05bb2-184">Stato codice HTTP</span><span class="sxs-lookup"><span data-stu-id="05bb2-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="05bb2-185">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="05bb2-185">Authentication</span></span>
<span data-ttu-id="05bb2-186">funzionalità di App per la logica di Hello consente toouse diversi tipi di autenticazione a fronte di endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="05bb2-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="05bb2-187">È possibile utilizzare l'autenticazione con hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, e  **[HTTP Webhook](connectors-native-webhook.md)**  connettori.</span><span class="sxs-lookup"><span data-stu-id="05bb2-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="05bb2-188">Hello seguenti tipi di autenticazione possono essere configurata:</span><span class="sxs-lookup"><span data-stu-id="05bb2-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="05bb2-189">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="05bb2-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="05bb2-190">Autenticazione con certificato client</span><span class="sxs-lookup"><span data-stu-id="05bb2-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="05bb2-191">Autenticazione OAuth di Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="05bb2-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="05bb2-192">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="05bb2-192">Basic authentication</span></span>

<span data-ttu-id="05bb2-193">Hello segue l'oggetto di autenticazione è necessaria l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="05bb2-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="05bb2-194">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="05bb2-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="05bb2-195">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="05bb2-195">Property name</span></span> | <span data-ttu-id="05bb2-196">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="05bb2-196">Data type</span></span> | <span data-ttu-id="05bb2-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05bb2-198">Type*</span><span class="sxs-lookup"><span data-stu-id="05bb2-198">Type*</span></span> |<span data-ttu-id="05bb2-199">type</span><span class="sxs-lookup"><span data-stu-id="05bb2-199">type</span></span> |<span data-ttu-id="05bb2-200">Tipo di autenticazione (deve essere `Basic` per l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="05bb2-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="05bb2-201">Username*</span><span class="sxs-lookup"><span data-stu-id="05bb2-201">Username*</span></span> |<span data-ttu-id="05bb2-202">username</span><span class="sxs-lookup"><span data-stu-id="05bb2-202">username</span></span> |<span data-ttu-id="05bb2-203">Tooauthenticate nome utente</span><span class="sxs-lookup"><span data-stu-id="05bb2-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="05bb2-204">Password*</span><span class="sxs-lookup"><span data-stu-id="05bb2-204">Password*</span></span> |<span data-ttu-id="05bb2-205">password</span><span class="sxs-lookup"><span data-stu-id="05bb2-205">password</span></span> |<span data-ttu-id="05bb2-206">Password tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="05bb2-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="05bb2-207">Se si desidera toouse una password che non può essere recuperata dalla definizione di hello, utilizzare un `securestring` parametro e hello `@parameters()`  
>  [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="05bb2-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="05bb2-208">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="05bb2-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="05bb2-209">Autenticazione con certificato client</span><span class="sxs-lookup"><span data-stu-id="05bb2-209">Client certificate authentication</span></span>

<span data-ttu-id="05bb2-210">oggetto di autenticazione seguenti Hello è necessaria per l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="05bb2-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="05bb2-211">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="05bb2-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="05bb2-212">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="05bb2-212">Property name</span></span> | <span data-ttu-id="05bb2-213">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="05bb2-213">Data type</span></span> | <span data-ttu-id="05bb2-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05bb2-215">Type*</span><span class="sxs-lookup"><span data-stu-id="05bb2-215">Type*</span></span> |<span data-ttu-id="05bb2-216">type</span><span class="sxs-lookup"><span data-stu-id="05bb2-216">type</span></span> |<span data-ttu-id="05bb2-217">tipo di autenticazione Hello (deve essere `ClientCertificate` per i certificati client SSL)</span><span class="sxs-lookup"><span data-stu-id="05bb2-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="05bb2-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="05bb2-218">PFX*</span></span> |<span data-ttu-id="05bb2-219">pfx</span><span class="sxs-lookup"><span data-stu-id="05bb2-219">pfx</span></span> |<span data-ttu-id="05bb2-220">contenuto con codifica Base64 Hello del file di scambio di informazioni personali (PFX) hello</span><span class="sxs-lookup"><span data-stu-id="05bb2-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="05bb2-221">Password*</span><span class="sxs-lookup"><span data-stu-id="05bb2-221">Password*</span></span> |<span data-ttu-id="05bb2-222">password</span><span class="sxs-lookup"><span data-stu-id="05bb2-222">password</span></span> |<span data-ttu-id="05bb2-223">Hello password tooaccess hello file PFX</span><span class="sxs-lookup"><span data-stu-id="05bb2-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="05bb2-224">un parametro che non sarà leggibile nella definizione di hello dopo il salvataggio di hello logica app toouse, è possibile utilizzare un `securestring` parametro e hello `@parameters()`  
>  [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="05bb2-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="05bb2-225">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="05bb2-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="05bb2-226">Autenticazione OAuth di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bb2-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="05bb2-227">Hello segue l'oggetto di autenticazione è necessaria per l'autenticazione OAuth di Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="05bb2-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="05bb2-228">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="05bb2-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="05bb2-229">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="05bb2-229">Property name</span></span> | <span data-ttu-id="05bb2-230">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="05bb2-230">Data type</span></span> | <span data-ttu-id="05bb2-231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05bb2-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05bb2-232">Type*</span><span class="sxs-lookup"><span data-stu-id="05bb2-232">Type*</span></span> |<span data-ttu-id="05bb2-233">type</span><span class="sxs-lookup"><span data-stu-id="05bb2-233">type</span></span> |<span data-ttu-id="05bb2-234">tipo di autenticazione Hello (deve essere `ActiveDirectoryOAuth` per OAuth di Active Directory di Azure)</span><span class="sxs-lookup"><span data-stu-id="05bb2-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="05bb2-235">Tenant*</span><span class="sxs-lookup"><span data-stu-id="05bb2-235">Tenant*</span></span> |<span data-ttu-id="05bb2-236">tenant</span><span class="sxs-lookup"><span data-stu-id="05bb2-236">tenant</span></span> |<span data-ttu-id="05bb2-237">Identificatore del tenant Hello per tenant hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bb2-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="05bb2-238">Pubblico*</span><span class="sxs-lookup"><span data-stu-id="05bb2-238">Audience*</span></span> |<span data-ttu-id="05bb2-239">audience</span><span class="sxs-lookup"><span data-stu-id="05bb2-239">audience</span></span> |<span data-ttu-id="05bb2-240">risorsa Hello toouse autorizzazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="05bb2-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="05bb2-241">Ad esempio: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="05bb2-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="05bb2-242">ID cliente*</span><span class="sxs-lookup"><span data-stu-id="05bb2-242">Client ID*</span></span> |<span data-ttu-id="05bb2-243">clientId</span><span class="sxs-lookup"><span data-stu-id="05bb2-243">clientId</span></span> |<span data-ttu-id="05bb2-244">Hello identificatore client per un'applicazione hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bb2-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="05bb2-245">Segreto*</span><span class="sxs-lookup"><span data-stu-id="05bb2-245">Secret*</span></span> |<span data-ttu-id="05bb2-246">secret</span><span class="sxs-lookup"><span data-stu-id="05bb2-246">secret</span></span> |<span data-ttu-id="05bb2-247">segreto Hello del client hello che sta richiedendo hello token</span><span class="sxs-lookup"><span data-stu-id="05bb2-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="05bb2-248">È possibile utilizzare un `securestring` parametro e hello `@parameters()` [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs) toouse un parametro che non sarà leggibile nella definizione di hello dopo il salvataggio.</span><span class="sxs-lookup"><span data-stu-id="05bb2-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="05bb2-249">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="05bb2-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="05bb2-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05bb2-250">Next steps</span></span>
<span data-ttu-id="05bb2-251">A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="05bb2-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="05bb2-252">È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="05bb2-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

