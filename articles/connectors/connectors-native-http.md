---
title: Comunicare con qualsiasi endpoint su HTTP - App per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="e075d-103">Introduzione all'azione HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-103">Get started with the HTTP action</span></span>

<span data-ttu-id="e075d-104">Con l'azione HTTP è possibile estendere i flussi di lavoro per l'organizzazione e comunicare con qualsiasi endpoint su HTTP.</span><span class="sxs-lookup"><span data-stu-id="e075d-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="e075d-105">È possibile:</span><span class="sxs-lookup"><span data-stu-id="e075d-105">You can:</span></span>

* <span data-ttu-id="e075d-106">Creare flussi di lavoro con app per la logica che si attivano (trigger) quando un sito Web gestito diventa inattivo.</span><span class="sxs-lookup"><span data-stu-id="e075d-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="e075d-107">Comunicare con qualsiasi endpoint su HTTP per estendere i flussi di lavoro ad altri servizi.</span><span class="sxs-lookup"><span data-stu-id="e075d-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="e075d-108">Per informazioni su come iniziare a usare un'azione HTTP in un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e075d-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="e075d-109">Usare un trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-109">Use the HTTP trigger</span></span>
<span data-ttu-id="e075d-110">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e075d-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="e075d-111">[Altre informazioni sui trigger](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e075d-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="e075d-112">Ecco una sequenza di esempio di come configurare un trigger HTTP nella finestra di progettazione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e075d-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="e075d-113">Aggiungere il trigger HTTP all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e075d-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="e075d-114">Specificare i parametri per l'endpoint HTTP di cui si vuole eseguire il polling.</span><span class="sxs-lookup"><span data-stu-id="e075d-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="e075d-115">Modificare l'intervallo di ricorrenza che stabilisce la frequenza del polling.</span><span class="sxs-lookup"><span data-stu-id="e075d-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="e075d-116">L'app per la logica ora si attiva con il contenuto restituito durante ogni controllo.</span><span class="sxs-lookup"><span data-stu-id="e075d-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![Trigger HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="e075d-118">Come funziona il trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-118">How the HTTP trigger works</span></span>

<span data-ttu-id="e075d-119">Il trigger HTTP invia una chiamata a un endpoint HTTP a intervalli ricorrenti.</span><span class="sxs-lookup"><span data-stu-id="e075d-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="e075d-120">Per impostazione predefinita, il codice di risposta HTTP inferiore a 300 genera l'esecuzione di un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e075d-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="e075d-121">Per specificare se deve essere attivata l'app per la logica, è possibile modificare l'app per la logica nella visualizzazione del codice e aggiungere una condizione che verrà valutata dopo la chiamata HTTP.</span><span class="sxs-lookup"><span data-stu-id="e075d-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="e075d-122">Di seguito è riportato un esempio di trigger HTTP che viene attivato quando il codice di stato restituito è maggiore di o uguale a `400`.</span><span class="sxs-lookup"><span data-stu-id="e075d-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

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

<span data-ttu-id="e075d-123">Tutti i dettagli sui parametri dei trigger HTTP sono disponibili in [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="e075d-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="e075d-124">Usare l'azione HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-124">Use the HTTP action</span></span>

<span data-ttu-id="e075d-125">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e075d-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="e075d-126">[Altre informazioni sulle azioni](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e075d-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="e075d-127">Scegliere **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="e075d-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="e075d-128">Nella casella di ricerca dell'azione digitare **http** per elencare le azioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="e075d-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Selezionare l'azione HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="e075d-130">Aggiungere i parametri richiesti per la chiamata HTTP.</span><span class="sxs-lookup"><span data-stu-id="e075d-130">Add any required parameters for the HTTP call.</span></span>
   
    ![Completare l'azione HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="e075d-132">Fare clic su **Salva** nella barra degli strumenti della finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="e075d-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="e075d-133">L'app per la logica viene salvata e pubblicata (attivata) nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="e075d-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="e075d-134">Trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-134">HTTP trigger</span></span>
<span data-ttu-id="e075d-135">Ecco i dettagli per il trigger supportato da questo connettore.</span><span class="sxs-lookup"><span data-stu-id="e075d-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="e075d-136">Il connettore HTTP supporta un solo trigger.</span><span class="sxs-lookup"><span data-stu-id="e075d-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="e075d-137">Trigger</span><span class="sxs-lookup"><span data-stu-id="e075d-137">Trigger</span></span> | <span data-ttu-id="e075d-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e075d-139">http</span><span class="sxs-lookup"><span data-stu-id="e075d-139">HTTP</span></span> |<span data-ttu-id="e075d-140">Esegue una chiamata HTTP e restituisce il contenuto della risposta.</span><span class="sxs-lookup"><span data-stu-id="e075d-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="e075d-141">Azione HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-141">HTTP action</span></span>
<span data-ttu-id="e075d-142">Ecco i dettagli per l'azione supportata da questo connettore.</span><span class="sxs-lookup"><span data-stu-id="e075d-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="e075d-143">Il connettore HTTP supporta una sola azione possibile.</span><span class="sxs-lookup"><span data-stu-id="e075d-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="e075d-144">Azione</span><span class="sxs-lookup"><span data-stu-id="e075d-144">Action</span></span> | <span data-ttu-id="e075d-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e075d-146">http</span><span class="sxs-lookup"><span data-stu-id="e075d-146">HTTP</span></span> |<span data-ttu-id="e075d-147">Esegue una chiamata HTTP e restituisce il contenuto della risposta.</span><span class="sxs-lookup"><span data-stu-id="e075d-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="e075d-148">Dettagli di HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-148">HTTP details</span></span>
<span data-ttu-id="e075d-149">La tabella seguente descrive i campi di input obbligatori e facoltativi per l'azione e i dettagli di output corrispondenti associati all'uso dell'azione.</span><span class="sxs-lookup"><span data-stu-id="e075d-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="e075d-150">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-150">HTTP request</span></span>
<span data-ttu-id="e075d-151">Di seguito sono riportati campi di input per l'azione, che esegue una richiesta HTTP in uscita.</span><span class="sxs-lookup"><span data-stu-id="e075d-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="e075d-152">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="e075d-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="e075d-153">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="e075d-153">Display name</span></span> | <span data-ttu-id="e075d-154">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="e075d-154">Property name</span></span> | <span data-ttu-id="e075d-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e075d-156">Metodo*</span><span class="sxs-lookup"><span data-stu-id="e075d-156">Method*</span></span> |<span data-ttu-id="e075d-157">statico</span><span class="sxs-lookup"><span data-stu-id="e075d-157">method</span></span> |<span data-ttu-id="e075d-158">Verbo HTTP da usare</span><span class="sxs-lookup"><span data-stu-id="e075d-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="e075d-159">URI*</span><span class="sxs-lookup"><span data-stu-id="e075d-159">URI*</span></span> |<span data-ttu-id="e075d-160">Uri</span><span class="sxs-lookup"><span data-stu-id="e075d-160">uri</span></span> |<span data-ttu-id="e075d-161">URI per la richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="e075d-162">Headers</span><span class="sxs-lookup"><span data-stu-id="e075d-162">Headers</span></span> |<span data-ttu-id="e075d-163">Headers</span><span class="sxs-lookup"><span data-stu-id="e075d-163">headers</span></span> |<span data-ttu-id="e075d-164">Un oggetto JSON delle intestazioni HTTP da includere</span><span class="sxs-lookup"><span data-stu-id="e075d-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="e075d-165">Corpo</span><span class="sxs-lookup"><span data-stu-id="e075d-165">Body</span></span> |<span data-ttu-id="e075d-166">Corpo</span><span class="sxs-lookup"><span data-stu-id="e075d-166">body</span></span> |<span data-ttu-id="e075d-167">Il corpo della richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-167">The HTTP request body</span></span> |
| <span data-ttu-id="e075d-168">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="e075d-168">Authentication</span></span> |<span data-ttu-id="e075d-169">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="e075d-169">authentication</span></span> |<span data-ttu-id="e075d-170">Dettagli nella sezione [Autenticazione](#authentication) .</span><span class="sxs-lookup"><span data-stu-id="e075d-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="e075d-171">Dettagli dell'output</span><span class="sxs-lookup"><span data-stu-id="e075d-171">Output details</span></span>
<span data-ttu-id="e075d-172">Di seguito sono riportati i dettagli di output per la risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="e075d-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="e075d-173">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="e075d-173">Property name</span></span> | <span data-ttu-id="e075d-174">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="e075d-174">Data type</span></span> | <span data-ttu-id="e075d-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e075d-176">headers</span><span class="sxs-lookup"><span data-stu-id="e075d-176">Headers</span></span> |<span data-ttu-id="e075d-177">object</span><span class="sxs-lookup"><span data-stu-id="e075d-177">object</span></span> |<span data-ttu-id="e075d-178">Intestazioni della risposta</span><span class="sxs-lookup"><span data-stu-id="e075d-178">Response headers</span></span> |
| <span data-ttu-id="e075d-179">Corpo</span><span class="sxs-lookup"><span data-stu-id="e075d-179">Body</span></span> |<span data-ttu-id="e075d-180">object</span><span class="sxs-lookup"><span data-stu-id="e075d-180">object</span></span> |<span data-ttu-id="e075d-181">Oggetto della risposta</span><span class="sxs-lookup"><span data-stu-id="e075d-181">Response object</span></span> |
| <span data-ttu-id="e075d-182">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="e075d-182">Status Code</span></span> |<span data-ttu-id="e075d-183">int</span><span class="sxs-lookup"><span data-stu-id="e075d-183">int</span></span> |<span data-ttu-id="e075d-184">Stato codice HTTP</span><span class="sxs-lookup"><span data-stu-id="e075d-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="e075d-185">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="e075d-185">Authentication</span></span>
<span data-ttu-id="e075d-186">La funzionalità App per la logica permette di usare diversi tipi di autenticazione per gli endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="e075d-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="e075d-187">Questo tipo di autenticazione può essere usato con i connettori **HTTP**, **[HTTP e Swagger](connectors-native-http-swagger.md)** e **[Webhook HTTP](connectors-native-webhook.md)**.</span><span class="sxs-lookup"><span data-stu-id="e075d-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="e075d-188">È possibile configurare i seguenti tipi di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="e075d-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="e075d-189">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="e075d-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="e075d-190">Autenticazione con certificato client</span><span class="sxs-lookup"><span data-stu-id="e075d-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="e075d-191">Autenticazione OAuth di Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="e075d-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="e075d-192">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="e075d-192">Basic authentication</span></span>

<span data-ttu-id="e075d-193">Per l'autenticazione di base è necessario l'oggetto di autenticazione seguente.</span><span class="sxs-lookup"><span data-stu-id="e075d-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="e075d-194">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="e075d-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="e075d-195">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="e075d-195">Property name</span></span> | <span data-ttu-id="e075d-196">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="e075d-196">Data type</span></span> | <span data-ttu-id="e075d-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e075d-198">Type*</span><span class="sxs-lookup"><span data-stu-id="e075d-198">Type*</span></span> |<span data-ttu-id="e075d-199">type</span><span class="sxs-lookup"><span data-stu-id="e075d-199">type</span></span> |<span data-ttu-id="e075d-200">Tipo di autenticazione (deve essere `Basic` per l'autenticazione di base)</span><span class="sxs-lookup"><span data-stu-id="e075d-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="e075d-201">Username*</span><span class="sxs-lookup"><span data-stu-id="e075d-201">Username*</span></span> |<span data-ttu-id="e075d-202">username</span><span class="sxs-lookup"><span data-stu-id="e075d-202">username</span></span> |<span data-ttu-id="e075d-203">Nome utente da autenticare</span><span class="sxs-lookup"><span data-stu-id="e075d-203">User name to authenticate</span></span> |
| <span data-ttu-id="e075d-204">Password*</span><span class="sxs-lookup"><span data-stu-id="e075d-204">Password*</span></span> |<span data-ttu-id="e075d-205">password</span><span class="sxs-lookup"><span data-stu-id="e075d-205">password</span></span> |<span data-ttu-id="e075d-206">Password da autenticare</span><span class="sxs-lookup"><span data-stu-id="e075d-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="e075d-207">Se si desidera usare una password che non può essere recuperata dalla definizione, usare un parametro `securestring` e la `@parameters()` 
> [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="e075d-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="e075d-208">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e075d-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="e075d-209">Autenticazione con certificato client</span><span class="sxs-lookup"><span data-stu-id="e075d-209">Client certificate authentication</span></span>

<span data-ttu-id="e075d-210">Per l'autenticazione con certificato client è necessario l'oggetto di autenticazione seguente.</span><span class="sxs-lookup"><span data-stu-id="e075d-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="e075d-211">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="e075d-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="e075d-212">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="e075d-212">Property name</span></span> | <span data-ttu-id="e075d-213">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="e075d-213">Data type</span></span> | <span data-ttu-id="e075d-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e075d-215">Type*</span><span class="sxs-lookup"><span data-stu-id="e075d-215">Type*</span></span> |<span data-ttu-id="e075d-216">type</span><span class="sxs-lookup"><span data-stu-id="e075d-216">type</span></span> |<span data-ttu-id="e075d-217">Tipo di autenticazione (deve essere `ClientCertificate` per i certificati client SSL)</span><span class="sxs-lookup"><span data-stu-id="e075d-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="e075d-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="e075d-218">PFX*</span></span> |<span data-ttu-id="e075d-219">pfx</span><span class="sxs-lookup"><span data-stu-id="e075d-219">pfx</span></span> |<span data-ttu-id="e075d-220">Contenuto con codifica Base 64 del file di scambio di informazioni personali (PFX, Personal Information Exchange)</span><span class="sxs-lookup"><span data-stu-id="e075d-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="e075d-221">Password*</span><span class="sxs-lookup"><span data-stu-id="e075d-221">Password*</span></span> |<span data-ttu-id="e075d-222">password</span><span class="sxs-lookup"><span data-stu-id="e075d-222">password</span></span> |<span data-ttu-id="e075d-223">La password per accedere al file PFX</span><span class="sxs-lookup"><span data-stu-id="e075d-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="e075d-224">Per usare un parametro che non sarà leggibile nella definizione dopo il salvataggio dell'app per la logica, è possibile usare un parametro `securestring` e la `@parameters()` 
> [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="e075d-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="e075d-225">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e075d-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="e075d-226">Autenticazione OAuth di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e075d-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="e075d-227">Per l'autenticazione OAuth di Azure Ad è necessario l'oggetto di autenticazione seguente.</span><span class="sxs-lookup"><span data-stu-id="e075d-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="e075d-228">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="e075d-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="e075d-229">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="e075d-229">Property name</span></span> | <span data-ttu-id="e075d-230">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="e075d-230">Data type</span></span> | <span data-ttu-id="e075d-231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e075d-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e075d-232">Type*</span><span class="sxs-lookup"><span data-stu-id="e075d-232">Type*</span></span> |<span data-ttu-id="e075d-233">type</span><span class="sxs-lookup"><span data-stu-id="e075d-233">type</span></span> |<span data-ttu-id="e075d-234">Tipo di autenticazione (deve essere `ActiveDirectoryOAuth` per OAuth di Azure AD)</span><span class="sxs-lookup"><span data-stu-id="e075d-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="e075d-235">Tenant*</span><span class="sxs-lookup"><span data-stu-id="e075d-235">Tenant*</span></span> |<span data-ttu-id="e075d-236">tenant</span><span class="sxs-lookup"><span data-stu-id="e075d-236">tenant</span></span> |<span data-ttu-id="e075d-237">L'identificatore del tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e075d-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="e075d-238">Pubblico*</span><span class="sxs-lookup"><span data-stu-id="e075d-238">Audience*</span></span> |<span data-ttu-id="e075d-239">audience</span><span class="sxs-lookup"><span data-stu-id="e075d-239">audience</span></span> |<span data-ttu-id="e075d-240">La risorsa per cui si sta richiedendo l'autorizzazione per l'uso.</span><span class="sxs-lookup"><span data-stu-id="e075d-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="e075d-241">Ad esempio: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="e075d-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="e075d-242">ID cliente*</span><span class="sxs-lookup"><span data-stu-id="e075d-242">Client ID*</span></span> |<span data-ttu-id="e075d-243">clientId</span><span class="sxs-lookup"><span data-stu-id="e075d-243">clientId</span></span> |<span data-ttu-id="e075d-244">Identificatore client per l'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="e075d-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="e075d-245">Segreto*</span><span class="sxs-lookup"><span data-stu-id="e075d-245">Secret*</span></span> |<span data-ttu-id="e075d-246">secret</span><span class="sxs-lookup"><span data-stu-id="e075d-246">secret</span></span> |<span data-ttu-id="e075d-247">Segreto del client che richiede il token</span><span class="sxs-lookup"><span data-stu-id="e075d-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="e075d-248">È possibile usare un parametro `securestring` e la [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs) `@parameters()` per usare un parametro che non sarà leggibile nella definizione dopo il salvataggio.</span><span class="sxs-lookup"><span data-stu-id="e075d-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="e075d-249">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e075d-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="e075d-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e075d-250">Next steps</span></span>
<span data-ttu-id="e075d-251">Provare ora a usare la piattaforma e [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e075d-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e075d-252">È possibile esplorare gli altri connettori disponibili nelle app per la logica esaminando l' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e075d-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

