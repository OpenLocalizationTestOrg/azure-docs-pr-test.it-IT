---
title: 'Azioni e trigger del flusso di lavoro: App per la logica di Azure | Microsoft Docs'
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="86f6e-102">Azioni e trigger del flusso di lavoro per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="86f6e-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="86f6e-103">Le app per la logica sono costituite da trigger e da azioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="86f6e-104">Sono disponibili sei tipi di trigger.</span><span class="sxs-lookup"><span data-stu-id="86f6e-104">There are six types of triggers.</span></span> <span data-ttu-id="86f6e-105">Ogni tipo ha un'interfaccia e un comportamento diversi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="86f6e-106">Per altre informazioni dettagliate, vedere il [linguaggio di definizione del flusso di lavoro](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="86f6e-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="86f6e-107">Per altre informazioni sui trigger e sulle azioni e su come usarli per compilare app per la logica per migliorare i processi e i flussi di lavoro aziendali, continuare la lettura.</span><span class="sxs-lookup"><span data-stu-id="86f6e-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="86f6e-108">Trigger</span><span class="sxs-lookup"><span data-stu-id="86f6e-108">Triggers</span></span>  

<span data-ttu-id="86f6e-109">Un trigger specifica le chiamate che possono avviare un'esecuzione del flusso di lavoro delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="86f6e-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="86f6e-110">Di seguito sono indicati i due diversi modi per avviare un'esecuzione del flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="86f6e-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="86f6e-111">Un trigger di poll</span><span class="sxs-lookup"><span data-stu-id="86f6e-111">A polling trigger</span></span>  

-   <span data-ttu-id="86f6e-112">Un trigger di push, chiamando l'[API REST del servizio di flusso di lavoro](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="86f6e-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="86f6e-113">Tutti i trigger contengono questi elementi di livello superiore:</span><span class="sxs-lookup"><span data-stu-id="86f6e-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="86f6e-114">Tipi e input dei trigger</span><span class="sxs-lookup"><span data-stu-id="86f6e-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="86f6e-115">È possibile usare questi tipi di trigger:</span><span class="sxs-lookup"><span data-stu-id="86f6e-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="86f6e-116">**Request** \- Imposta l'app per la logica come endpoint per le chiamate</span><span class="sxs-lookup"><span data-stu-id="86f6e-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="86f6e-117">**Recurrence** \- Esegue l'attivazione in base a una pianificazione definita</span><span class="sxs-lookup"><span data-stu-id="86f6e-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="86f6e-118">**HTTP** \- Esegue il polling di un endpoint Web HTTP.</span><span class="sxs-lookup"><span data-stu-id="86f6e-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="86f6e-119">L'endpoint HTTP deve essere conforme a uno specifico contratto di attivazione, usando un modello asincrono 202 o restituendo una matrice</span><span class="sxs-lookup"><span data-stu-id="86f6e-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="86f6e-120">**ApiConnection** \- Esegue il polling come il trigger HTTP, ma sfrutta le [API gestite da Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="86f6e-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="86f6e-121">**HTTPWebhook** \- Apre un endpoint, analogamente al trigger Manual, ma chiama anche un URL specificato per la registrazione e l'annullamento della registrazione</span><span class="sxs-lookup"><span data-stu-id="86f6e-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="86f6e-122">**ApiConnectionWebhook** \- Funziona come il trigger HTTPWebhook, sfruttando le API gestite da Microsoft</span><span class="sxs-lookup"><span data-stu-id="86f6e-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="86f6e-123">Ogni tipo di trigger ha un diverso set di **input** che ne definisce il comportamento.</span><span class="sxs-lookup"><span data-stu-id="86f6e-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="86f6e-124">Trigger di richiesta</span><span class="sxs-lookup"><span data-stu-id="86f6e-124">Request trigger</span></span>  

<span data-ttu-id="86f6e-125">Questo trigger funge da endpoint chiamato tramite una richiesta HTTP per richiamare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="86f6e-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="86f6e-126">Un trigger request è simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="86f6e-127">Esiste anche una proprietà facoltativa denominata **schema**:</span><span class="sxs-lookup"><span data-stu-id="86f6e-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="86f6e-128">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-128">Element name</span></span>|<span data-ttu-id="86f6e-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="86f6e-129">Required</span></span>|<span data-ttu-id="86f6e-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="86f6e-131">schema</span><span class="sxs-lookup"><span data-stu-id="86f6e-131">schema</span></span>|<span data-ttu-id="86f6e-132">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-132">No</span></span>|<span data-ttu-id="86f6e-133">Schema JSON che convalida la richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="86f6e-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="86f6e-134">È utile per indicare le proprietà a cui fare riferimento nei passaggi successivi del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="86f6e-135">Per richiamare questo endpoint, è necessario chiamare l'API *listCallbackUrl*.</span><span class="sxs-lookup"><span data-stu-id="86f6e-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="86f6e-136">Vedere [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows) (API REST del servizio di flusso di lavoro).</span><span class="sxs-lookup"><span data-stu-id="86f6e-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="86f6e-137">Trigger Recurrence</span><span class="sxs-lookup"><span data-stu-id="86f6e-137">Recurrence trigger</span></span>  

<span data-ttu-id="86f6e-138">Un trigger Recurrence viene eseguito in base a una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="86f6e-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="86f6e-139">Tale trigger può essere simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="86f6e-140">Come si può osservare, è un modo semplice per eseguire un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="86f6e-141">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-141">Element name</span></span>|<span data-ttu-id="86f6e-142">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="86f6e-142">Required</span></span>|<span data-ttu-id="86f6e-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="86f6e-144">frequency</span><span class="sxs-lookup"><span data-stu-id="86f6e-144">frequency</span></span>|<span data-ttu-id="86f6e-145">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-145">Yes</span></span>|<span data-ttu-id="86f6e-146">Frequenza con cui viene eseguito il trigger.</span><span class="sxs-lookup"><span data-stu-id="86f6e-146">How often the trigger executes.</span></span> <span data-ttu-id="86f6e-147">Usare solo uno di questi possibili valori: second, minute, hour, day, week, month o year</span><span class="sxs-lookup"><span data-stu-id="86f6e-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="86f6e-148">interval</span><span class="sxs-lookup"><span data-stu-id="86f6e-148">interval</span></span>|<span data-ttu-id="86f6e-149">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-149">Yes</span></span>|<span data-ttu-id="86f6e-150">Intervallo della frequenza specificata per la ricorrenza</span><span class="sxs-lookup"><span data-stu-id="86f6e-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="86f6e-151">startTime</span><span class="sxs-lookup"><span data-stu-id="86f6e-151">startTime</span></span>|<span data-ttu-id="86f6e-152">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-152">No</span></span>|<span data-ttu-id="86f6e-153">Se viene fornito un valore startTime senza una differenza dall'ora UTC, viene usato tale valore timeZone.</span><span class="sxs-lookup"><span data-stu-id="86f6e-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="86f6e-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="86f6e-154">timeZone</span></span>|<span data-ttu-id="86f6e-155">no</span><span class="sxs-lookup"><span data-stu-id="86f6e-155">no</span></span>|<span data-ttu-id="86f6e-156">Se viene fornito un valore startTime senza una differenza dall'ora UTC, viene usato tale valore timeZone.</span><span class="sxs-lookup"><span data-stu-id="86f6e-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="86f6e-157">È anche possibile pianificare l'avvio dell'esecuzione di un trigger in futuro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="86f6e-158">Se, ad esempio, si vuole avviare un report settimanale ogni lunedì, è possibile pianificare l'avvio dell'app per la logica ogni lunedì creando il trigger seguente:</span><span class="sxs-lookup"><span data-stu-id="86f6e-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="86f6e-159">Trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="86f6e-159">HTTP trigger</span></span>  

<span data-ttu-id="86f6e-160">I trigger HTTP eseguono il polling di un endpoint specificato e controllano la risposta per determinare se il flusso di lavoro deve essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="86f6e-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="86f6e-161">L'oggetto inputs usa il set di parametri necessari per costruire una chiamata HTTP:</span><span class="sxs-lookup"><span data-stu-id="86f6e-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="86f6e-162">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-162">Element name</span></span>|<span data-ttu-id="86f6e-163">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="86f6e-163">Required</span></span>|<span data-ttu-id="86f6e-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-164">Description</span></span>|<span data-ttu-id="86f6e-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="86f6e-166">statico</span><span class="sxs-lookup"><span data-stu-id="86f6e-166">method</span></span>|<span data-ttu-id="86f6e-167">sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-167">yes</span></span>|<span data-ttu-id="86f6e-168">Può essere uno dei metodi HTTP seguenti: GET, POST, PUT, DELETE, PATCH o HEAD</span><span class="sxs-lookup"><span data-stu-id="86f6e-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="86f6e-169">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-169">String</span></span>|  
|<span data-ttu-id="86f6e-170">Uri</span><span class="sxs-lookup"><span data-stu-id="86f6e-170">uri</span></span>|<span data-ttu-id="86f6e-171">sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-171">yes</span></span>|<span data-ttu-id="86f6e-172">Endpoint http o https che viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="86f6e-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="86f6e-173">Il valore massimo è di 2 kilobyte.</span><span class="sxs-lookup"><span data-stu-id="86f6e-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="86f6e-174">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-174">String</span></span>|  
|<span data-ttu-id="86f6e-175">query</span><span class="sxs-lookup"><span data-stu-id="86f6e-175">queries</span></span>|<span data-ttu-id="86f6e-176">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-176">No</span></span>|<span data-ttu-id="86f6e-177">Oggetto che rappresenta i parametri di query da aggiungere all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="86f6e-178">`"queries" : { "api-version": "2015-02-01" }`, ad esempio, aggiunge `?api-version=2015-02-01` all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="86f6e-179">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-179">Object</span></span>|  
|<span data-ttu-id="86f6e-180">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-180">headers</span></span>|<span data-ttu-id="86f6e-181">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-181">No</span></span>|<span data-ttu-id="86f6e-182">Oggetto che rappresenta ogni intestazione inviata alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="86f6e-183">Ad esempio, per impostare il linguaggio e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="86f6e-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="86f6e-184">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-184">Object</span></span>|  
|<span data-ttu-id="86f6e-185">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-185">body</span></span>|<span data-ttu-id="86f6e-186">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-186">No</span></span>|<span data-ttu-id="86f6e-187">Oggetto che rappresenta il payload inviato all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="86f6e-188">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-188">Object</span></span>|  
|<span data-ttu-id="86f6e-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="86f6e-189">retryPolicy</span></span>|<span data-ttu-id="86f6e-190">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-190">No</span></span>|<span data-ttu-id="86f6e-191">Oggetto che consente di personalizzare il comportamento in caso di nuovo tentativo per gli errori 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="86f6e-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="86f6e-192">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-192">Object</span></span>|  
|<span data-ttu-id="86f6e-193">authentication</span><span class="sxs-lookup"><span data-stu-id="86f6e-193">authentication</span></span>|<span data-ttu-id="86f6e-194">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-194">No</span></span>|<span data-ttu-id="86f6e-195">Rappresenta il metodo con cui autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="86f6e-196">Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="86f6e-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="86f6e-197">Oltre all'utilità di pianificazione, esiste un'altra proprietà supportata: `authority`. Per impostazione predefinita, questo valore è `https://login.windows.net` quando non viene specificato, ma è possibile usare un gruppo di destinatari diverso, ad esempio `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="86f6e-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="86f6e-198">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-198">Object</span></span>|  
  
<span data-ttu-id="86f6e-199">Con il trigger HTTP, l'API HTTP deve essere conforme a un modello specifico per poter interagire correttamente con l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="86f6e-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="86f6e-200">Sono necessari i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="86f6e-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="86f6e-201">Response</span><span class="sxs-lookup"><span data-stu-id="86f6e-201">Response</span></span>|<span data-ttu-id="86f6e-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="86f6e-203">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="86f6e-203">Status code</span></span>|<span data-ttu-id="86f6e-204">Il codice di stato 200 \(OK\) attiva un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="86f6e-205">Nessun altro codice di stato attiva un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="86f6e-206">Intestazione Retry\-after</span><span class="sxs-lookup"><span data-stu-id="86f6e-206">Retry\-after header</span></span>|<span data-ttu-id="86f6e-207">Numero di secondi prima che l'app per la logica esegua di nuovo il polling dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="86f6e-208">Intestazione Location</span><span class="sxs-lookup"><span data-stu-id="86f6e-208">Location header</span></span>|<span data-ttu-id="86f6e-209">URL da chiamare al successivo intervallo di polling.</span><span class="sxs-lookup"><span data-stu-id="86f6e-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="86f6e-210">Se non è specificato, viene usato l'URL originale.</span><span class="sxs-lookup"><span data-stu-id="86f6e-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="86f6e-211">Di seguito sono riportati alcuni esempi di comportamenti diversi a seconda del tipo di richiesta:</span><span class="sxs-lookup"><span data-stu-id="86f6e-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="86f6e-212">Codice della risposta</span><span class="sxs-lookup"><span data-stu-id="86f6e-212">Response code</span></span>|<span data-ttu-id="86f6e-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="86f6e-213">Retry\-After</span></span>|<span data-ttu-id="86f6e-214">Comportamento</span><span class="sxs-lookup"><span data-stu-id="86f6e-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="86f6e-215">200</span><span class="sxs-lookup"><span data-stu-id="86f6e-215">200</span></span>|<span data-ttu-id="86f6e-216">\(nessuna\)</span><span class="sxs-lookup"><span data-stu-id="86f6e-216">\(none\)</span></span>|<span data-ttu-id="86f6e-217">Trigger non valido. Retry\-After è obbligatorio, altrimenti il motore non esegue mai il polling per la richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="86f6e-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="86f6e-218">202</span><span class="sxs-lookup"><span data-stu-id="86f6e-218">202</span></span>|<span data-ttu-id="86f6e-219">60</span><span class="sxs-lookup"><span data-stu-id="86f6e-219">60</span></span>|<span data-ttu-id="86f6e-220">Non attiva il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-220">Do not trigger the workflow.</span></span> <span data-ttu-id="86f6e-221">Verrà eseguito un altro tentativo entro un minuto.</span><span class="sxs-lookup"><span data-stu-id="86f6e-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="86f6e-222">200</span><span class="sxs-lookup"><span data-stu-id="86f6e-222">200</span></span>|<span data-ttu-id="86f6e-223">10</span><span class="sxs-lookup"><span data-stu-id="86f6e-223">10</span></span>|<span data-ttu-id="86f6e-224">Esegue il flusso di lavoro e verifica di nuovo la disponibilità di altri contenuti entro 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="86f6e-225">400</span><span class="sxs-lookup"><span data-stu-id="86f6e-225">400</span></span>|<span data-ttu-id="86f6e-226">\(nessuna\)</span><span class="sxs-lookup"><span data-stu-id="86f6e-226">\(none\)</span></span>|<span data-ttu-id="86f6e-227">Richiesta non valida, non esegue il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="86f6e-228">Se non è definito alcun **criterio per i tentativi**, vengono usati i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="86f6e-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="86f6e-229">Dopo che è stato raggiunto il numero di tentativi, il trigger non è più valido.</span><span class="sxs-lookup"><span data-stu-id="86f6e-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="86f6e-230">500</span><span class="sxs-lookup"><span data-stu-id="86f6e-230">500</span></span>|<span data-ttu-id="86f6e-231">\(nessuna\)</span><span class="sxs-lookup"><span data-stu-id="86f6e-231">\(none\)</span></span>|<span data-ttu-id="86f6e-232">Errore del server, non esegue il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="86f6e-233">Se non è definito alcun **criterio per i tentativi**, vengono usati i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="86f6e-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="86f6e-234">Dopo che è stato raggiunto il numero di tentativi, il trigger non è più valido.</span><span class="sxs-lookup"><span data-stu-id="86f6e-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="86f6e-235">Gli output di un trigger HTTP sono simili a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="86f6e-236">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-236">Element name</span></span>|<span data-ttu-id="86f6e-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-237">Description</span></span>|<span data-ttu-id="86f6e-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="86f6e-239">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-239">headers</span></span>|<span data-ttu-id="86f6e-240">Intestazioni della risposta http.</span><span class="sxs-lookup"><span data-stu-id="86f6e-240">The headers of the http response.</span></span>|<span data-ttu-id="86f6e-241">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-241">Object</span></span>|  
|<span data-ttu-id="86f6e-242">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-242">body</span></span>|<span data-ttu-id="86f6e-243">Corpo della risposta http.</span><span class="sxs-lookup"><span data-stu-id="86f6e-243">The body of the http response.</span></span>|<span data-ttu-id="86f6e-244">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="86f6e-245">Trigger ApiConnection</span><span class="sxs-lookup"><span data-stu-id="86f6e-245">API Connection trigger</span></span>  

<span data-ttu-id="86f6e-246">Il trigger ApiConnection è simile al trigger HTTP dal punto di vista della funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="86f6e-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="86f6e-247">I parametri per identificare l'azione sono tuttavia diversi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="86f6e-248">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="86f6e-249">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-249">Element name</span></span>|<span data-ttu-id="86f6e-250">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-250">Required</span></span>|<span data-ttu-id="86f6e-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-251">Type</span></span>|<span data-ttu-id="86f6e-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-253">host</span><span class="sxs-lookup"><span data-stu-id="86f6e-253">host</span></span>|<span data-ttu-id="86f6e-254">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-254">Yes</span></span>||<span data-ttu-id="86f6e-255">ID e gateway ospitato da ApiApp.</span><span class="sxs-lookup"><span data-stu-id="86f6e-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="86f6e-256">statico</span><span class="sxs-lookup"><span data-stu-id="86f6e-256">method</span></span>|<span data-ttu-id="86f6e-257">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-257">Yes</span></span>|<span data-ttu-id="86f6e-258">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-258">String</span></span>|<span data-ttu-id="86f6e-259">Può essere uno dei metodi HTTP seguenti: **GET**, **POST**, **PUT**, **DELETE**, **PATCH** o **HEAD**</span><span class="sxs-lookup"><span data-stu-id="86f6e-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="86f6e-260">query</span><span class="sxs-lookup"><span data-stu-id="86f6e-260">queries</span></span>|<span data-ttu-id="86f6e-261">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-261">No</span></span>|<span data-ttu-id="86f6e-262">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-262">Object</span></span>|<span data-ttu-id="86f6e-263">Rappresenta i parametri di query da aggiungere all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="86f6e-264">`"queries" : { "api-version": "2015-02-01" }`, ad esempio, aggiunge `?api-version=2015-02-01` all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="86f6e-265">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-265">headers</span></span>|<span data-ttu-id="86f6e-266">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-266">No</span></span>|<span data-ttu-id="86f6e-267">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-267">Object</span></span>|<span data-ttu-id="86f6e-268">Rappresenta ogni intestazione inviata alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="86f6e-269">Ad esempio, per impostare il linguaggio e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="86f6e-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="86f6e-270">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-270">body</span></span>|<span data-ttu-id="86f6e-271">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-271">No</span></span>|<span data-ttu-id="86f6e-272">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-272">Object</span></span>|<span data-ttu-id="86f6e-273">Rappresenta il payload inviato all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="86f6e-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="86f6e-274">retryPolicy</span></span>|<span data-ttu-id="86f6e-275">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-275">No</span></span>|<span data-ttu-id="86f6e-276">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-276">Object</span></span>|<span data-ttu-id="86f6e-277">Consente di personalizzare il comportamento in caso di nuovo tentativo per gli errori 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="86f6e-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="86f6e-278">authentication</span><span class="sxs-lookup"><span data-stu-id="86f6e-278">authentication</span></span>|<span data-ttu-id="86f6e-279">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-279">No</span></span>|<span data-ttu-id="86f6e-280">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-280">Object</span></span>|<span data-ttu-id="86f6e-281">Rappresenta il metodo con cui autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="86f6e-282">Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="86f6e-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="86f6e-283">Le proprietà dell'host sono:</span><span class="sxs-lookup"><span data-stu-id="86f6e-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="86f6e-284">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-284">Element name</span></span>|<span data-ttu-id="86f6e-285">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="86f6e-285">Required</span></span>|<span data-ttu-id="86f6e-286">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="86f6e-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="86f6e-287">api runtimeUrl</span></span>|<span data-ttu-id="86f6e-288">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-288">Yes</span></span>|<span data-ttu-id="86f6e-289">Endpoint dell'API gestita.</span><span class="sxs-lookup"><span data-stu-id="86f6e-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="86f6e-290">connection name</span><span class="sxs-lookup"><span data-stu-id="86f6e-290">connection name</span></span>||<span data-ttu-id="86f6e-291">Deve essere un riferimento a un parametro denominato `$connection` ed è il nome della connessione API gestita usata dal flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="86f6e-292">Gli output di un trigger ApiConnection sono:</span><span class="sxs-lookup"><span data-stu-id="86f6e-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="86f6e-293">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-293">Element name</span></span>|<span data-ttu-id="86f6e-294">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-294">Type</span></span>|<span data-ttu-id="86f6e-295">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="86f6e-296">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-296">headers</span></span>|<span data-ttu-id="86f6e-297">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-297">Object</span></span>|<span data-ttu-id="86f6e-298">Intestazioni della risposta http.</span><span class="sxs-lookup"><span data-stu-id="86f6e-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="86f6e-299">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-299">body</span></span>|<span data-ttu-id="86f6e-300">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-300">Object</span></span>|<span data-ttu-id="86f6e-301">Corpo della risposta http.</span><span class="sxs-lookup"><span data-stu-id="86f6e-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="86f6e-302">Trigger HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="86f6e-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="86f6e-303">Il trigger HTTPWebhook apre un endpoint, analogamente al trigger manual, ma il trigger HTTPWebhook chiama anche un URL specificato per la registrazione e l'annullamento della registrazione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="86f6e-304">Ecco un esempio di come si presenta un trigger HTTPWebhook:</span><span class="sxs-lookup"><span data-stu-id="86f6e-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="86f6e-305">Molte di queste sezioni sono facoltative e il comportamento del webhook dipende dalle sezioni che vengono fornite o omesse.</span><span class="sxs-lookup"><span data-stu-id="86f6e-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="86f6e-306">Le proprietà di un webhook sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="86f6e-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="86f6e-307">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-307">Element name</span></span>|<span data-ttu-id="86f6e-308">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="86f6e-308">Required</span></span>|<span data-ttu-id="86f6e-309">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="86f6e-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="86f6e-310">subscribe</span></span>|<span data-ttu-id="86f6e-311">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-311">No</span></span>|<span data-ttu-id="86f6e-312">Richiesta in uscita chiamata quando il trigger viene creato ed esegue la registrazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="86f6e-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="86f6e-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="86f6e-313">unsubscribe</span></span>|<span data-ttu-id="86f6e-314">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-314">No</span></span>|<span data-ttu-id="86f6e-315">Richiesta in uscita quando il trigger viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="86f6e-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="86f6e-316">**Subscribe** è la chiamata in uscita effettuata per iniziare ad ascoltare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="86f6e-317">Questa chiamata inizia con lo stesso set di parametri delle normali azioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="86f6e-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="86f6e-318">Questa chiamata in uscita viene effettuata ogni volta che il flusso di lavoro viene modificato, ad esempio quando vengono aggiornate le credenziali o cambiano i parametri di input del trigger.</span><span class="sxs-lookup"><span data-stu-id="86f6e-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="86f6e-319">Per supportare questa chiamata, è disponibile una nuova funzione: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="86f6e-320">Questa funzione restituisce un URL univoco per il trigger specifico nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="86f6e-321">Rappresenta l'identificatore univoco per gli endpoint che usano l'API REST del servizio.</span><span class="sxs-lookup"><span data-stu-id="86f6e-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="86f6e-322">**Unsubscribe** viene chiamata quando un'operazione rende questo trigger non valido, tra cui:</span><span class="sxs-lookup"><span data-stu-id="86f6e-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="86f6e-323">Eliminazione o disabilitazione del trigger</span><span class="sxs-lookup"><span data-stu-id="86f6e-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="86f6e-324">Eliminazione o disabilitazione del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="86f6e-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="86f6e-325">Eliminazione o disabilitazione della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="86f6e-326">L'app per la logica chiama automaticamente l'azione unsubscribe.</span><span class="sxs-lookup"><span data-stu-id="86f6e-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="86f6e-327">I parametri di questa funzione sono gli stessi del trigger HTTP.</span><span class="sxs-lookup"><span data-stu-id="86f6e-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="86f6e-328">Gli output del trigger HTTPWebhook sono i contenuti della richiesta in ingresso:</span><span class="sxs-lookup"><span data-stu-id="86f6e-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="86f6e-329">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-329">Element name</span></span>|<span data-ttu-id="86f6e-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-330">Type</span></span>|<span data-ttu-id="86f6e-331">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="86f6e-332">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-332">headers</span></span>|<span data-ttu-id="86f6e-333">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-333">Object</span></span>|<span data-ttu-id="86f6e-334">Intestazioni della richiesta http.</span><span class="sxs-lookup"><span data-stu-id="86f6e-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="86f6e-335">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-335">body</span></span>|<span data-ttu-id="86f6e-336">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-336">Object</span></span>|<span data-ttu-id="86f6e-337">Corpo della richiesta http.</span><span class="sxs-lookup"><span data-stu-id="86f6e-337">The body of the http request.</span></span>|  

<span data-ttu-id="86f6e-338">I limiti per un'azione webhook possono essere specificati nello stesso modo dei [limiti asincroni HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="86f6e-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="86f6e-339">Condizioni</span><span class="sxs-lookup"><span data-stu-id="86f6e-339">Conditions</span></span>  

<span data-ttu-id="86f6e-340">Per qualsiasi trigger, è possibile usare una o più condizioni per determinare se il flusso di lavoro deve essere eseguito o meno.</span><span class="sxs-lookup"><span data-stu-id="86f6e-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="86f6e-341">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="86f6e-342">In questo caso, il report viene attivato solo mentre il parametro `sendReports` del flusso di lavoro è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="86f6e-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="86f6e-343">Le condizioni infine possono fare riferimento al codice di stato del trigger.</span><span class="sxs-lookup"><span data-stu-id="86f6e-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="86f6e-344">È possibile, ad esempio, avviare un flusso di lavoro solo quando il sito Web restituisce un codice di stato 500, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="86f6e-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="86f6e-345">Quando un'espressione fa riferimento al codice di stato del trigger \(in qualsiasi modo\), il comportamento predefinito \(attivazione solo con 200 \(OK\)\) viene sostituito.</span><span class="sxs-lookup"><span data-stu-id="86f6e-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="86f6e-346">Se, ad esempio, si vuole eseguire l'attivazione sia con il codice di stato 200 che con il codice di stato 201, è necessario includere `@or(equals(triggers().code, 200),equals(triggers().code,201))` come condizione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="86f6e-347">Avviare più esecuzioni per una richiesta</span><span class="sxs-lookup"><span data-stu-id="86f6e-347">Start multiple runs for a request</span></span>

<span data-ttu-id="86f6e-348">Per avviare più esecuzioni per una singola richiesta, `splitOn` è utile, ad esempio, quando si vuole eseguire il polling di un endpoint che può avere più elementi nuovi tra gli intervalli di polling.</span><span class="sxs-lookup"><span data-stu-id="86f6e-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="86f6e-349">Con `splitOn`, si specifica la proprietà nel payload della risposta contenente le matrici di elementi, ognuno dei quali verrà usato per avviare un'esecuzione del trigger.</span><span class="sxs-lookup"><span data-stu-id="86f6e-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="86f6e-350">Si consideri ad esempio uno scenario in cui un'API restituisce la risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="86f6e-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="86f6e-351">L'app per la logica richiede solo il contenuto di Rows, quindi è possibile costruire il trigger come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="86f6e-352">Nella definizione del flusso di lavoro `@triggerBody().name` restituisce quindi `mycoolrow` per la prima esecuzione e `another row` per la seconda esecuzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="86f6e-353">Gli output del trigger sono simili a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="86f6e-354">Se quindi si usa `SplitOn`, non è possibile ottenere le proprietà esterne alla matrice, in questo caso il campo `Status`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="86f6e-355">In questo esempio viene usato l'operatore `?` per poter evitare un errore se la proprietà `Rows` non è presente.</span><span class="sxs-lookup"><span data-stu-id="86f6e-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="86f6e-356">Istanza di esecuzione singola</span><span class="sxs-lookup"><span data-stu-id="86f6e-356">Single run instance</span></span>

<span data-ttu-id="86f6e-357">È possibile configurare trigger con una proprietà recurrence in modo che vengano attivati solo se tutte le esecuzioni attive sono state completate.</span><span class="sxs-lookup"><span data-stu-id="86f6e-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="86f6e-358">Se una ricorrenza pianificata si verifica mentre è in corso un'esecuzione, il trigger viene ignorato e attende fino al successivo intervallo di ricorrenza pianificata prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="86f6e-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="86f6e-359">È possibile configurate questa impostazione tramite le opzioni dell'operazione:</span><span class="sxs-lookup"><span data-stu-id="86f6e-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="86f6e-360">Tipi e input</span><span class="sxs-lookup"><span data-stu-id="86f6e-360">Types and inputs</span></span>  

<span data-ttu-id="86f6e-361">Esistono molti tipi di azioni, ognuna con un comportamento univoco.</span><span class="sxs-lookup"><span data-stu-id="86f6e-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="86f6e-362">Le azioni di raccolta possono contenere diverse altre azioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="86f6e-363">Azioni standard</span><span class="sxs-lookup"><span data-stu-id="86f6e-363">Standard actions</span></span>  

-   <span data-ttu-id="86f6e-364">**HTTP** Questa azione chiama un endpoint Web HTTP.</span><span class="sxs-lookup"><span data-stu-id="86f6e-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="86f6e-365">**ApiConnection** \- Questa azione si comporta come l'azione HTTP, ma usa le API gestite da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86f6e-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="86f6e-366">**ApiConnectionWebhook** \- Come HTTPWebhook, ma usa le API gestite da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86f6e-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="86f6e-367">**Response** \- Questa azione definisce una risposta per una chiamata in ingresso.</span><span class="sxs-lookup"><span data-stu-id="86f6e-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="86f6e-368">**Wait** \- Questa semplice azione attende per un intervallo di tempo fisso o fino a un'ora specifica.</span><span class="sxs-lookup"><span data-stu-id="86f6e-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="86f6e-369">**Workflow** \- Questa azione rappresenta un flusso di lavoro annidato.</span><span class="sxs-lookup"><span data-stu-id="86f6e-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="86f6e-370">**Function** \- Questa azione rappresenta una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="86f6e-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="86f6e-371">Azioni di raccolta</span><span class="sxs-lookup"><span data-stu-id="86f6e-371">Collection actions</span></span>

-   <span data-ttu-id="86f6e-372">**Scope** \- Questa azione è un raggruppamento logico di altre azioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="86f6e-373">**Condition** \- Questa azione restituisce un'espressione ed esegue il corrispondente ramo di risultati.</span><span class="sxs-lookup"><span data-stu-id="86f6e-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="86f6e-374">**ForEach** \- Questa azione di riproduzione a ciclo continuo scorre una matrice ed esegue azioni interne per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="86f6e-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="86f6e-375">**Until** \- Questa azione di riproduzione a ciclo continuo esegue azioni interne finché una condizione non restituisce true.</span><span class="sxs-lookup"><span data-stu-id="86f6e-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="86f6e-376">Ogni tipo di azione ha un set diverso di **input** che definiscono il comportamento di un'azione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="86f6e-377">Azione HTTP</span><span class="sxs-lookup"><span data-stu-id="86f6e-377">HTTP action</span></span>  

<span data-ttu-id="86f6e-378">Le azioni HTTP chiamano un endpoint specificato e controllano la risposta per determinare se il flusso di lavoro deve essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="86f6e-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="86f6e-379">L'oggetto **inputs** usa il set di parametri necessari per costruire la chiamata HTTP:</span><span class="sxs-lookup"><span data-stu-id="86f6e-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="86f6e-380">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-380">Element name</span></span>|<span data-ttu-id="86f6e-381">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-381">Required</span></span>|<span data-ttu-id="86f6e-382">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-382">Type</span></span>|<span data-ttu-id="86f6e-383">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-384">statico</span><span class="sxs-lookup"><span data-stu-id="86f6e-384">method</span></span>|<span data-ttu-id="86f6e-385">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-385">Yes</span></span>|<span data-ttu-id="86f6e-386">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-386">String</span></span>|<span data-ttu-id="86f6e-387">Può essere uno dei metodi HTTP seguenti: **GET**, **POST**, **PUT**, **DELETE**, **PATCH** o **HEAD**</span><span class="sxs-lookup"><span data-stu-id="86f6e-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="86f6e-388">Uri</span><span class="sxs-lookup"><span data-stu-id="86f6e-388">uri</span></span>|<span data-ttu-id="86f6e-389">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-389">Yes</span></span>|<span data-ttu-id="86f6e-390">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-390">String</span></span>|<span data-ttu-id="86f6e-391">Endpoint http o https che viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="86f6e-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="86f6e-392">La lunghezza massima è 2 kilobyte.</span><span class="sxs-lookup"><span data-stu-id="86f6e-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="86f6e-393">query</span><span class="sxs-lookup"><span data-stu-id="86f6e-393">queries</span></span>|<span data-ttu-id="86f6e-394">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-394">No</span></span>|<span data-ttu-id="86f6e-395">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-395">Object</span></span>|<span data-ttu-id="86f6e-396">Rappresenta i parametri di query da aggiungere all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="86f6e-397">`"queries" : { "api-version": "2015-02-01" }`, ad esempio, aggiunge `?api-version=2015-02-01` all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="86f6e-398">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-398">headers</span></span>|<span data-ttu-id="86f6e-399">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-399">No</span></span>|<span data-ttu-id="86f6e-400">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-400">Object</span></span>|<span data-ttu-id="86f6e-401">Rappresenta ogni intestazione inviata alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="86f6e-402">Ad esempio, per impostare il linguaggio e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="86f6e-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="86f6e-403">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-403">body</span></span>|<span data-ttu-id="86f6e-404">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-404">No</span></span>|<span data-ttu-id="86f6e-405">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-405">Object</span></span>|<span data-ttu-id="86f6e-406">Rappresenta il payload inviato all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="86f6e-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="86f6e-407">retryPolicy</span></span>|<span data-ttu-id="86f6e-408">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-408">No</span></span>|<span data-ttu-id="86f6e-409">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-409">Object</span></span>|<span data-ttu-id="86f6e-410">Consente di personalizzare il comportamento in caso di nuovo tentativo per gli errori 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="86f6e-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="86f6e-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="86f6e-411">operationsOptions</span></span>|<span data-ttu-id="86f6e-412">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-412">No</span></span>|<span data-ttu-id="86f6e-413">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-413">String</span></span>|<span data-ttu-id="86f6e-414">Definisce il set di comportamenti speciali di cui eseguire l'override.</span><span class="sxs-lookup"><span data-stu-id="86f6e-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="86f6e-415">authentication</span><span class="sxs-lookup"><span data-stu-id="86f6e-415">authentication</span></span>|<span data-ttu-id="86f6e-416">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-416">No</span></span>|<span data-ttu-id="86f6e-417">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-417">Object</span></span>|<span data-ttu-id="86f6e-418">Rappresenta il metodo con cui autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="86f6e-419">Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="86f6e-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="86f6e-420">Oltre all'utilità di pianificazione, esiste un'altra proprietà supportata, `authority`,</span><span class="sxs-lookup"><span data-stu-id="86f6e-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="86f6e-421">che, per impostazione predefinita, è `https://login.windows.net` quando non è specificata, ma è possibile usare un gruppo di destinatari diverso, ad esempio `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="86f6e-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="86f6e-422">Le azioni HTTP \(e di connessione API\) supportano i criteri per i tentativi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="86f6e-423">I criteri per i tentativi vengono applicati agli errori intermittenti, caratterizzati dai codici di stato HTTP 408, 429 e 5xx, oltre che alle eccezioni per la connettività.</span><span class="sxs-lookup"><span data-stu-id="86f6e-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="86f6e-424">Questi criteri vengono descritti con l'oggetto *retryPolicy* definito di seguito:</span><span class="sxs-lookup"><span data-stu-id="86f6e-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="86f6e-425">L'intervallo tra tentativi viene specificato nel formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="86f6e-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="86f6e-426">Questo intervallo ha un valore predefinito e minimo di 20 secondi, mentre il valore massimo è di un'ora.</span><span class="sxs-lookup"><span data-stu-id="86f6e-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="86f6e-427">Il numero predefinito e massimo di tentativi è pari a quattro ore.</span><span class="sxs-lookup"><span data-stu-id="86f6e-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="86f6e-428">Se la definizione dei criteri per i tentativi non è specificata, viene usata una strategia `fixed` con valori di intervallo e di numero di tentativi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="86f6e-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="86f6e-429">Per disabilitare i criteri per i tentativi, impostare il tipo su `None`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="86f6e-430">L'azione seguente, ad esempio, prova a recuperare di nuovo le ultime novità per due volte, se si verificano errori intermittenti, per un totale di tre esecuzioni, con un ritardo di 30 secondi tra un tentativo e l'altro:</span><span class="sxs-lookup"><span data-stu-id="86f6e-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="86f6e-431">Modelli asincroni</span><span class="sxs-lookup"><span data-stu-id="86f6e-431">Asynchronous patterns</span></span>

<span data-ttu-id="86f6e-432">Per impostazione predefinita, tutte le azioni basate su HTTP supportano il modello di operazione asincrono standard.</span><span class="sxs-lookup"><span data-stu-id="86f6e-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="86f6e-433">Se quindi il server remoto indica che la richiesta viene accettata per l'elaborazione con una risposta 202 \(Accepted\), il motore di App per la logica continua il polling dell'URL specificato nell'intestazione location della risposta fino a raggiungere uno stato terminale \(una risposta diversa da 202\).</span><span class="sxs-lookup"><span data-stu-id="86f6e-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="86f6e-434">Per disabilitare il comportamento asincrono descritto prima, impostare un'opzione `DisableAsyncPattern` negli input dell'azione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="86f6e-435">In questo caso, l'output dell'azione si basa sulla risposta 202 iniziale dal server.</span><span class="sxs-lookup"><span data-stu-id="86f6e-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="86f6e-436">Limiti asincroni</span><span class="sxs-lookup"><span data-stu-id="86f6e-436">Asynchronous Limits</span></span>

<span data-ttu-id="86f6e-437">La durata di un modello asincrono può essere limitata a un intervallo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="86f6e-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="86f6e-438">Se l'intervallo di tempo trascorre senza raggiungere uno stato terminale, lo stato dell'azione verrà contrassegnato come `Cancelled` con il codice `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="86f6e-439">Il timeout per il limite è specificato nel formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="86f6e-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="86f6e-440">I limiti possono essere specificati con la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="86f6e-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="86f6e-441">Connessione API</span><span class="sxs-lookup"><span data-stu-id="86f6e-441">API Connection</span></span>  

<span data-ttu-id="86f6e-442">La connessione API è un'azione che fa riferimento a un connettore gestito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86f6e-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="86f6e-443">Questa azione richiede un riferimento a una connessione valida e informazioni sull'API e sui parametri obbligatori.</span><span class="sxs-lookup"><span data-stu-id="86f6e-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="86f6e-444">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="86f6e-444">Element name</span></span>|<span data-ttu-id="86f6e-445">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-445">Required</span></span>|<span data-ttu-id="86f6e-446">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-446">Type</span></span>|<span data-ttu-id="86f6e-447">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-448">host</span><span class="sxs-lookup"><span data-stu-id="86f6e-448">host</span></span>|<span data-ttu-id="86f6e-449">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-449">Yes</span></span>|<span data-ttu-id="86f6e-450">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-450">Object</span></span>|<span data-ttu-id="86f6e-451">Rappresenta le informazioni sul connettore, ad esempio il valore di runtimeUrl e il riferimento all'oggetto connection</span><span class="sxs-lookup"><span data-stu-id="86f6e-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="86f6e-452">statico</span><span class="sxs-lookup"><span data-stu-id="86f6e-452">method</span></span>|<span data-ttu-id="86f6e-453">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-453">Yes</span></span>|<span data-ttu-id="86f6e-454">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-454">String</span></span>|<span data-ttu-id="86f6e-455">Può essere uno dei metodi HTTP seguenti: **GET**, **POST**, **PUT**, **DELETE**, **PATCH** o **HEAD**</span><span class="sxs-lookup"><span data-stu-id="86f6e-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="86f6e-456">path</span><span class="sxs-lookup"><span data-stu-id="86f6e-456">path</span></span>|<span data-ttu-id="86f6e-457">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-457">Yes</span></span>|<span data-ttu-id="86f6e-458">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-458">String</span></span>|<span data-ttu-id="86f6e-459">Percorso dell'operazione API.</span><span class="sxs-lookup"><span data-stu-id="86f6e-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="86f6e-460">query</span><span class="sxs-lookup"><span data-stu-id="86f6e-460">queries</span></span>|<span data-ttu-id="86f6e-461">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-461">No</span></span>|<span data-ttu-id="86f6e-462">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-462">Object</span></span>|<span data-ttu-id="86f6e-463">Rappresenta i parametri di query da aggiungere all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="86f6e-464">`"queries" : { "api-version": "2015-02-01" }`, ad esempio, aggiunge `?api-version=2015-02-01` all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="86f6e-465">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-465">headers</span></span>|<span data-ttu-id="86f6e-466">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-466">No</span></span>|<span data-ttu-id="86f6e-467">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-467">Object</span></span>|<span data-ttu-id="86f6e-468">Rappresenta ogni intestazione inviata alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="86f6e-469">Ad esempio, per impostare il linguaggio e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="86f6e-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="86f6e-470">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-470">body</span></span>|<span data-ttu-id="86f6e-471">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-471">No</span></span>|<span data-ttu-id="86f6e-472">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-472">Object</span></span>|<span data-ttu-id="86f6e-473">Rappresenta il payload inviato all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="86f6e-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="86f6e-474">retryPolicy</span></span>|<span data-ttu-id="86f6e-475">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-475">No</span></span>|<span data-ttu-id="86f6e-476">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-476">Object</span></span>|<span data-ttu-id="86f6e-477">Consente di personalizzare il comportamento in caso di nuovo tentativo per gli errori 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="86f6e-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="86f6e-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="86f6e-478">operationsOptions</span></span>|<span data-ttu-id="86f6e-479">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-479">No</span></span>|<span data-ttu-id="86f6e-480">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-480">String</span></span>|<span data-ttu-id="86f6e-481">Definisce il set di comportamenti speciali di cui eseguire l'override.</span><span class="sxs-lookup"><span data-stu-id="86f6e-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="86f6e-482">Azione webhook di connessione API</span><span class="sxs-lookup"><span data-stu-id="86f6e-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="86f6e-483">I limiti per un'azione webhook possono essere specificati nello stesso modo dei [limiti asincroni HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="86f6e-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="86f6e-484">Azione di risposta</span><span class="sxs-lookup"><span data-stu-id="86f6e-484">Response action</span></span>  

<span data-ttu-id="86f6e-485">Questo tipo di azione contiene l'intero payload della risposta da una richiesta HTTP e include statusCode, body e headers:</span><span class="sxs-lookup"><span data-stu-id="86f6e-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="86f6e-486">L'azione response ha particolari restrizioni che non si applicano alle altre azioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="86f6e-487">In particolare:</span><span class="sxs-lookup"><span data-stu-id="86f6e-487">Specifically:</span></span>  
  
-   <span data-ttu-id="86f6e-488">Le azioni response non possono essere parallele in una definizione perché è necessaria una risposta deterministica alla richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="86f6e-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="86f6e-489">Se un'azione response viene raggiunta dopo che la richiesta in ingresso ha ricevuto una risposta, l'azione viene considerata non riuscita \(conflict\) e di conseguenza l'esecuzione è `Failed`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="86f6e-490">Un flusso di lavoro con azioni response non può avere `splitOn` nel trigger perché una chiamata genera più esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="86f6e-491">Verrà quindi convalidato quando il flusso è PUT e genererà una richiesta non valida.</span><span class="sxs-lookup"><span data-stu-id="86f6e-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="86f6e-492">Azione wait</span><span class="sxs-lookup"><span data-stu-id="86f6e-492">Wait action</span></span>  

<span data-ttu-id="86f6e-493">L'azione `wait` sospende l'esecuzione del flusso di lavoro per l'intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="86f6e-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="86f6e-494">Per attendere 15 minuti, ad esempio, è possibile usare questo frammento:</span><span class="sxs-lookup"><span data-stu-id="86f6e-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="86f6e-495">In alternativa, per attendere fino a un determinato momento, è possibile usare questo esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="86f6e-496">La durata dell'attesa può essere specificata usando l'oggetto **interval** o l'oggetto **until**, ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="86f6e-497">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-497">Name</span></span>|<span data-ttu-id="86f6e-498">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-498">Required</span></span>|<span data-ttu-id="86f6e-499">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-499">Type</span></span>|<span data-ttu-id="86f6e-500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-501">interval</span><span class="sxs-lookup"><span data-stu-id="86f6e-501">interval</span></span>|<span data-ttu-id="86f6e-502">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-502">No</span></span>|<span data-ttu-id="86f6e-503">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-503">Object</span></span>|<span data-ttu-id="86f6e-504">Durata dell'attesa basata su un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="86f6e-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="86f6e-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="86f6e-505">interval unit</span></span>|<span data-ttu-id="86f6e-506">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-506">Yes</span></span>|<span data-ttu-id="86f6e-507">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-507">String</span></span>|<span data-ttu-id="86f6e-508">Uno di questi intervalli: second, minute, hour, day, week, month, year.</span><span class="sxs-lookup"><span data-stu-id="86f6e-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="86f6e-509">interval count</span><span class="sxs-lookup"><span data-stu-id="86f6e-509">interval count</span></span>|<span data-ttu-id="86f6e-510">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-510">Yes</span></span>|<span data-ttu-id="86f6e-511">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-511">String</span></span>|<span data-ttu-id="86f6e-512">Durata basata sull'unità interna specificata.</span><span class="sxs-lookup"><span data-stu-id="86f6e-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="86f6e-513">until</span><span class="sxs-lookup"><span data-stu-id="86f6e-513">until</span></span>|<span data-ttu-id="86f6e-514">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-514">No</span></span>|<span data-ttu-id="86f6e-515">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-515">Object</span></span>|<span data-ttu-id="86f6e-516">Durata dell'attesa basata su data e ora.</span><span class="sxs-lookup"><span data-stu-id="86f6e-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="86f6e-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="86f6e-517">until timestamp</span></span>|<span data-ttu-id="86f6e-518">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-518">Yes</span></span>|<span data-ttu-id="86f6e-519">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-519">String</span></span>|<span data-ttu-id="86f6e-520">Data e ora in UTC in cui l'attesa scade.</span><span class="sxs-lookup"><span data-stu-id="86f6e-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="86f6e-521">Azione di query</span><span class="sxs-lookup"><span data-stu-id="86f6e-521">Query action</span></span>

<span data-ttu-id="86f6e-522">L'azione `query` consente di filtrare una matrice in base a una condizione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="86f6e-523">Per selezionare numeri maggiori di 2, ad esempio, è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="86f6e-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="86f6e-524">L'output dell'azione `query` è una matrice con elementi della matrice di input che soddisfano la condizione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="86f6e-525">Se nessun valore soddisfa la condizione `where`, il risultato è una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="86f6e-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="86f6e-526">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-526">Name</span></span>|<span data-ttu-id="86f6e-527">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-527">Required</span></span>|<span data-ttu-id="86f6e-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-528">Type</span></span>|<span data-ttu-id="86f6e-529">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="86f6e-530">from</span><span class="sxs-lookup"><span data-stu-id="86f6e-530">from</span></span>|<span data-ttu-id="86f6e-531">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-531">Yes</span></span>|<span data-ttu-id="86f6e-532">Array</span><span class="sxs-lookup"><span data-stu-id="86f6e-532">Array</span></span>|<span data-ttu-id="86f6e-533">Matrice di origine.</span><span class="sxs-lookup"><span data-stu-id="86f6e-533">The source array.</span></span>|
|<span data-ttu-id="86f6e-534">dove</span><span class="sxs-lookup"><span data-stu-id="86f6e-534">where</span></span>|<span data-ttu-id="86f6e-535">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-535">Yes</span></span>|<span data-ttu-id="86f6e-536">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-536">String</span></span>|<span data-ttu-id="86f6e-537">Condizione da applicare a ogni elemento della matrice di origine.</span><span class="sxs-lookup"><span data-stu-id="86f6e-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="86f6e-538">Seleziona azione</span><span class="sxs-lookup"><span data-stu-id="86f6e-538">Select action</span></span>

<span data-ttu-id="86f6e-539">L'azione `select` consente di proiettare ogni elemento dell'array in un nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="86f6e-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="86f6e-540">Ad esempio, per convertire un array di numeri in un array di oggetti è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="86f6e-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="86f6e-541">L'output dell'azione `select` è un array con la stessa cardinalità dell'array di input, con ogni elemento trasformato secondo quanto definito dalla proprietà `select`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="86f6e-542">Se l'input è un array vuoto, lo sarà anche l'output.</span><span class="sxs-lookup"><span data-stu-id="86f6e-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="86f6e-543">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-543">Name</span></span>|<span data-ttu-id="86f6e-544">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-544">Required</span></span>|<span data-ttu-id="86f6e-545">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-545">Type</span></span>|<span data-ttu-id="86f6e-546">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="86f6e-547">from</span><span class="sxs-lookup"><span data-stu-id="86f6e-547">from</span></span>|<span data-ttu-id="86f6e-548">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-548">Yes</span></span>|<span data-ttu-id="86f6e-549">Array</span><span class="sxs-lookup"><span data-stu-id="86f6e-549">Array</span></span>|<span data-ttu-id="86f6e-550">Matrice di origine.</span><span class="sxs-lookup"><span data-stu-id="86f6e-550">The source array.</span></span>|
|<span data-ttu-id="86f6e-551">seleziona</span><span class="sxs-lookup"><span data-stu-id="86f6e-551">select</span></span>|<span data-ttu-id="86f6e-552">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-552">Yes</span></span>|<span data-ttu-id="86f6e-553">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="86f6e-553">Any</span></span>|<span data-ttu-id="86f6e-554">La proiezione da applicare a ogni elemento dell'array di origine.</span><span class="sxs-lookup"><span data-stu-id="86f6e-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="86f6e-555">Azione terminate</span><span class="sxs-lookup"><span data-stu-id="86f6e-555">Terminate action</span></span>

<span data-ttu-id="86f6e-556">L'azione terminate arresta l'esecuzione del flusso di lavoro, interrompendo eventuali azioni in elaborazione e ignorando le azioni rimanenti.</span><span class="sxs-lookup"><span data-stu-id="86f6e-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="86f6e-557">Per terminare un'esecuzione con stato **Failed**, ad esempio, è possibile usare il frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="86f6e-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="86f6e-558">Le azioni già completate non sono interessate dall'azione terminate.</span><span class="sxs-lookup"><span data-stu-id="86f6e-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="86f6e-559">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-559">Name</span></span>|<span data-ttu-id="86f6e-560">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-560">Required</span></span>|<span data-ttu-id="86f6e-561">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-561">Type</span></span>|<span data-ttu-id="86f6e-562">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="86f6e-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="86f6e-563">runStatus</span></span>|<span data-ttu-id="86f6e-564">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-564">Yes</span></span>|<span data-ttu-id="86f6e-565">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-565">String</span></span>|<span data-ttu-id="86f6e-566">Stato dell'esecuzione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-566">The target run status.</span></span> <span data-ttu-id="86f6e-567">**Failed** o **Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="86f6e-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="86f6e-568">runError</span><span class="sxs-lookup"><span data-stu-id="86f6e-568">runError</span></span>|<span data-ttu-id="86f6e-569">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-569">No</span></span>|<span data-ttu-id="86f6e-570">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-570">Object</span></span>|<span data-ttu-id="86f6e-571">Dettagli dell'errore.</span><span class="sxs-lookup"><span data-stu-id="86f6e-571">The error details.</span></span> <span data-ttu-id="86f6e-572">Supportato solo quando **runStatus** è impostato su **Failed**.</span><span class="sxs-lookup"><span data-stu-id="86f6e-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="86f6e-573">runError code</span><span class="sxs-lookup"><span data-stu-id="86f6e-573">runError code</span></span>|<span data-ttu-id="86f6e-574">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-574">No</span></span>|<span data-ttu-id="86f6e-575">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-575">String</span></span>|<span data-ttu-id="86f6e-576">Codice errore di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-576">The run error code.</span></span>|
|<span data-ttu-id="86f6e-577">runError message</span><span class="sxs-lookup"><span data-stu-id="86f6e-577">runError message</span></span>|<span data-ttu-id="86f6e-578">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-578">No</span></span>|<span data-ttu-id="86f6e-579">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-579">String</span></span>|<span data-ttu-id="86f6e-580">Messaggio di errore di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="86f6e-581">Azione compose</span><span class="sxs-lookup"><span data-stu-id="86f6e-581">Compose action</span></span>

<span data-ttu-id="86f6e-582">L'azione compose consente di costruire un oggetto arbitrario.</span><span class="sxs-lookup"><span data-stu-id="86f6e-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="86f6e-583">L'output dell'azione compose è il risultato della valutazione degli input.</span><span class="sxs-lookup"><span data-stu-id="86f6e-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="86f6e-584">È possibile, ad esempio, usare l'azione compose per unire gli output di più azioni:</span><span class="sxs-lookup"><span data-stu-id="86f6e-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="86f6e-585">L'azione **Compose** può essere usata per costruire qualsiasi output, inclusi oggetti, matrici e altri tipi supportati a livello nativo dalle app per la logica, ad esempio file XML e binari.</span><span class="sxs-lookup"><span data-stu-id="86f6e-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="86f6e-586">azione Tabella</span><span class="sxs-lookup"><span data-stu-id="86f6e-586">Table action</span></span>

<span data-ttu-id="86f6e-587">`table` consente di convertire una matrice di elementi in una tabella **CSV** o **HTML**.</span><span class="sxs-lookup"><span data-stu-id="86f6e-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="86f6e-588">Presumere che @triggerBody() sia</span><span class="sxs-lookup"><span data-stu-id="86f6e-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="86f6e-589">Lasciare che l'azione venga definita come</span><span class="sxs-lookup"><span data-stu-id="86f6e-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="86f6e-590">L'elemento sopra darebbe</span><span class="sxs-lookup"><span data-stu-id="86f6e-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="86f6e-591">id</span><span class="sxs-lookup"><span data-stu-id="86f6e-591">id</span></span></th><th><span data-ttu-id="86f6e-592">name</span><span class="sxs-lookup"><span data-stu-id="86f6e-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="86f6e-593">0</span><span class="sxs-lookup"><span data-stu-id="86f6e-593">0</span></span></td><td><span data-ttu-id="86f6e-594">mele</span><span class="sxs-lookup"><span data-stu-id="86f6e-594">apples</span></span></td></tr><tr><td><span data-ttu-id="86f6e-595">1</span><span class="sxs-lookup"><span data-stu-id="86f6e-595">1</span></span></td><td><span data-ttu-id="86f6e-596">arance</span><span class="sxs-lookup"><span data-stu-id="86f6e-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="86f6e-597">"</span><span class="sxs-lookup"><span data-stu-id="86f6e-597">"</span></span>

<span data-ttu-id="86f6e-598">Per personalizzare la tabella, è possibile specificare le colonne in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="86f6e-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="86f6e-599">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="86f6e-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="86f6e-600">L'elemento sopra darebbe</span><span class="sxs-lookup"><span data-stu-id="86f6e-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="86f6e-601">ottenere ID</span><span class="sxs-lookup"><span data-stu-id="86f6e-601">produce id</span></span></th><th><span data-ttu-id="86f6e-602">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="86f6e-603">0</span><span class="sxs-lookup"><span data-stu-id="86f6e-603">0</span></span></td><td><span data-ttu-id="86f6e-604">mele fresche</span><span class="sxs-lookup"><span data-stu-id="86f6e-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="86f6e-605">1</span><span class="sxs-lookup"><span data-stu-id="86f6e-605">1</span></span></td><td><span data-ttu-id="86f6e-606">arance fresche</span><span class="sxs-lookup"><span data-stu-id="86f6e-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="86f6e-607">"</span><span class="sxs-lookup"><span data-stu-id="86f6e-607">"</span></span>

<span data-ttu-id="86f6e-608">Se il valore della proprietà `from` è un array vuoto, l'output sarà una tabella vuota.</span><span class="sxs-lookup"><span data-stu-id="86f6e-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="86f6e-609">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-609">Name</span></span>|<span data-ttu-id="86f6e-610">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-610">Required</span></span>|<span data-ttu-id="86f6e-611">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-611">Type</span></span>|<span data-ttu-id="86f6e-612">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="86f6e-613">from</span><span class="sxs-lookup"><span data-stu-id="86f6e-613">from</span></span>|<span data-ttu-id="86f6e-614">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-614">Yes</span></span>|<span data-ttu-id="86f6e-615">Array</span><span class="sxs-lookup"><span data-stu-id="86f6e-615">Array</span></span>|<span data-ttu-id="86f6e-616">Matrice di origine.</span><span class="sxs-lookup"><span data-stu-id="86f6e-616">The source array.</span></span>|
|<span data-ttu-id="86f6e-617">format</span><span class="sxs-lookup"><span data-stu-id="86f6e-617">format</span></span>|<span data-ttu-id="86f6e-618">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-618">Yes</span></span>|<span data-ttu-id="86f6e-619">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-619">String</span></span>|<span data-ttu-id="86f6e-620">Il formato, **CSV** o **HTML**.</span><span class="sxs-lookup"><span data-stu-id="86f6e-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="86f6e-621">columns</span><span class="sxs-lookup"><span data-stu-id="86f6e-621">columns</span></span>|<span data-ttu-id="86f6e-622">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-622">No</span></span>|<span data-ttu-id="86f6e-623">Array</span><span class="sxs-lookup"><span data-stu-id="86f6e-623">Array</span></span>|<span data-ttu-id="86f6e-624">Le colonne.</span><span class="sxs-lookup"><span data-stu-id="86f6e-624">The columns.</span></span> <span data-ttu-id="86f6e-625">Consente di sostituire la forma predefinita della tabella.</span><span class="sxs-lookup"><span data-stu-id="86f6e-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="86f6e-626">intestazione di colonna</span><span class="sxs-lookup"><span data-stu-id="86f6e-626">column header</span></span>|<span data-ttu-id="86f6e-627">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-627">No</span></span>|<span data-ttu-id="86f6e-628">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-628">String</span></span>|<span data-ttu-id="86f6e-629">L'intestazione della colonna.</span><span class="sxs-lookup"><span data-stu-id="86f6e-629">The header of the column.</span></span>|
|<span data-ttu-id="86f6e-630">valore colonna</span><span class="sxs-lookup"><span data-stu-id="86f6e-630">column value</span></span>|<span data-ttu-id="86f6e-631">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-631">Yes</span></span>|<span data-ttu-id="86f6e-632">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-632">String</span></span>|<span data-ttu-id="86f6e-633">Il valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="86f6e-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="86f6e-634">Azione workflow</span><span class="sxs-lookup"><span data-stu-id="86f6e-634">Workflow action</span></span>   

|<span data-ttu-id="86f6e-635">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-635">Name</span></span>|<span data-ttu-id="86f6e-636">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-636">Required</span></span>|<span data-ttu-id="86f6e-637">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-637">Type</span></span>|<span data-ttu-id="86f6e-638">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-639">host id</span><span class="sxs-lookup"><span data-stu-id="86f6e-639">host id</span></span>|<span data-ttu-id="86f6e-640">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-640">Yes</span></span>|<span data-ttu-id="86f6e-641">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-641">String</span></span>|<span data-ttu-id="86f6e-642">ID risorsa del flusso di lavoro che si vuole chiamare.</span><span class="sxs-lookup"><span data-stu-id="86f6e-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="86f6e-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="86f6e-643">host triggerName</span></span>|<span data-ttu-id="86f6e-644">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-644">Yes</span></span>|<span data-ttu-id="86f6e-645">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-645">String</span></span>|<span data-ttu-id="86f6e-646">Nome del trigger che si vuole richiamare.</span><span class="sxs-lookup"><span data-stu-id="86f6e-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="86f6e-647">query</span><span class="sxs-lookup"><span data-stu-id="86f6e-647">queries</span></span>|<span data-ttu-id="86f6e-648">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-648">No</span></span>|<span data-ttu-id="86f6e-649">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-649">Object</span></span>|<span data-ttu-id="86f6e-650">Rappresenta i parametri di query da aggiungere all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="86f6e-651">`"queries" : { "api-version": "2015-02-01" }`, ad esempio, aggiunge `?api-version=2015-02-01` all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="86f6e-652">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-652">headers</span></span>|<span data-ttu-id="86f6e-653">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-653">No</span></span>|<span data-ttu-id="86f6e-654">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-654">Object</span></span>|<span data-ttu-id="86f6e-655">Rappresenta ogni intestazione inviata alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="86f6e-656">Ad esempio, per impostare il linguaggio e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="86f6e-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="86f6e-657">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-657">body</span></span>|<span data-ttu-id="86f6e-658">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-658">No</span></span>|<span data-ttu-id="86f6e-659">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-659">Object</span></span>|<span data-ttu-id="86f6e-660">Rappresenta il payload inviato all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="86f6e-661">Poiché viene eseguito un controllo dell'accesso sul flusso di lavoro \(più in particolare, sul trigger\), è necessario l'accesso al flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="86f6e-662">Gli output dell'azione `workflow` si basano su quanto definito nell'azione `response` nel flusso di lavoro figlio.</span><span class="sxs-lookup"><span data-stu-id="86f6e-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="86f6e-663">Se non sono state definite azioni `response`, gli output sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="86f6e-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="86f6e-664">Azione delle funzioni</span><span class="sxs-lookup"><span data-stu-id="86f6e-664">Function action</span></span>   

|<span data-ttu-id="86f6e-665">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-665">Name</span></span>|<span data-ttu-id="86f6e-666">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-666">Required</span></span>|<span data-ttu-id="86f6e-667">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-667">Type</span></span>|<span data-ttu-id="86f6e-668">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-669">function id</span><span class="sxs-lookup"><span data-stu-id="86f6e-669">function id</span></span>|<span data-ttu-id="86f6e-670">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-670">Yes</span></span>|<span data-ttu-id="86f6e-671">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-671">String</span></span>|<span data-ttu-id="86f6e-672">ID risorsa della funzione che si vuole richiamare.</span><span class="sxs-lookup"><span data-stu-id="86f6e-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="86f6e-673">statico</span><span class="sxs-lookup"><span data-stu-id="86f6e-673">method</span></span>|<span data-ttu-id="86f6e-674">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-674">No</span></span>|<span data-ttu-id="86f6e-675">String</span><span class="sxs-lookup"><span data-stu-id="86f6e-675">String</span></span>|<span data-ttu-id="86f6e-676">Il metodo HTTP utilizzato per richiamare la funzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="86f6e-677">Per impostazione predefinita, è `POST` quando non è specificato.</span><span class="sxs-lookup"><span data-stu-id="86f6e-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="86f6e-678">query</span><span class="sxs-lookup"><span data-stu-id="86f6e-678">queries</span></span>|<span data-ttu-id="86f6e-679">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-679">No</span></span>|<span data-ttu-id="86f6e-680">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-680">Object</span></span>|<span data-ttu-id="86f6e-681">Rappresenta i parametri di query da aggiungere all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="86f6e-682">`"queries" : { "api-version": "2015-02-01" }`, ad esempio, aggiunge `?api-version=2015-02-01` all'URL.</span><span class="sxs-lookup"><span data-stu-id="86f6e-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="86f6e-683">headers</span><span class="sxs-lookup"><span data-stu-id="86f6e-683">headers</span></span>|<span data-ttu-id="86f6e-684">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-684">No</span></span>|<span data-ttu-id="86f6e-685">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-685">Object</span></span>|<span data-ttu-id="86f6e-686">Rappresenta ogni intestazione inviata alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="86f6e-687">Ad esempio, per impostare il linguaggio e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="86f6e-688">body</span><span class="sxs-lookup"><span data-stu-id="86f6e-688">body</span></span>|<span data-ttu-id="86f6e-689">No</span><span class="sxs-lookup"><span data-stu-id="86f6e-689">No</span></span>|<span data-ttu-id="86f6e-690">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-690">Object</span></span>|<span data-ttu-id="86f6e-691">Rappresenta il payload inviato all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="86f6e-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="86f6e-692">Quando si salva l'app per la logica, vengono eseguiti alcuni controlli sulla funzione a cui si fa riferimento:</span><span class="sxs-lookup"><span data-stu-id="86f6e-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="86f6e-693">È necessario disporre dell'accesso alla funzione.</span><span class="sxs-lookup"><span data-stu-id="86f6e-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="86f6e-694">È consentito solo il trigger HTTP standard o il trigger webhook JSON generico.</span><span class="sxs-lookup"><span data-stu-id="86f6e-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="86f6e-695">Non deve essere presente alcuna route definita.</span><span class="sxs-lookup"><span data-stu-id="86f6e-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="86f6e-696">Sono consentiti solo i livelli di autorizzazione "funzione" e "anonimo".</span><span class="sxs-lookup"><span data-stu-id="86f6e-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="86f6e-697">L'URL del trigger viene recuperato, memorizzato nella cache e usato durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="86f6e-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="86f6e-698">Pertanto, se qualsiasi operazione invalida l'URL memorizzato nella cache, l'azione non riesce durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="86f6e-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="86f6e-699">Per risolvere il problema, salvare di nuovo l'app per la logica. In questo modo, l'app per la logica verrà recuperata e l'URL del trigger verrà memorizzato nuovamente nella cache.</span><span class="sxs-lookup"><span data-stu-id="86f6e-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="86f6e-700">Azioni di raccolta (ambiti e cicli)</span><span class="sxs-lookup"><span data-stu-id="86f6e-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="86f6e-701">Alcuni tipi di azioni possono contenere azioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="86f6e-702">È possibile fare riferimento alle azioni di riferimento in una raccolta direttamente all'esterno della raccolta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="86f6e-703">Se si è definito `http` in un ambito, `@body('http')` è ancora valido in qualsiasi punto del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="86f6e-704">Le azioni in una raccolta possono essere eseguite (`runAfter`) solo dopo le altre azioni nella stessa raccolta.</span><span class="sxs-lookup"><span data-stu-id="86f6e-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="86f6e-705">Azione scope</span><span class="sxs-lookup"><span data-stu-id="86f6e-705">Scope action</span></span>

<span data-ttu-id="86f6e-706">L'azione `scope` consente di raggruppare logicamente le azioni in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="86f6e-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="86f6e-707">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-707">Name</span></span>|<span data-ttu-id="86f6e-708">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-708">Required</span></span>|<span data-ttu-id="86f6e-709">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-709">Type</span></span>|<span data-ttu-id="86f6e-710">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-711">Azioni</span><span class="sxs-lookup"><span data-stu-id="86f6e-711">actions</span></span>|<span data-ttu-id="86f6e-712">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-712">Yes</span></span>|<span data-ttu-id="86f6e-713">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-713">Object</span></span>|<span data-ttu-id="86f6e-714">Azioni interne da eseguire nell'ambito</span><span class="sxs-lookup"><span data-stu-id="86f6e-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="86f6e-715">Azione ForEach</span><span class="sxs-lookup"><span data-stu-id="86f6e-715">ForEach action</span></span>

<span data-ttu-id="86f6e-716">Questa azione di riproduzione a ciclo continuo scorre una matrice ed esegue azioni interne per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="86f6e-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="86f6e-717">Per impostazione predefinita, il ciclo foreach viene eseguito in parallelo (20 esecuzioni in parallelo per volta).</span><span class="sxs-lookup"><span data-stu-id="86f6e-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="86f6e-718">È possibile impostare regole di esecuzione usando il parametro `operationOptions`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="86f6e-719">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-719">Name</span></span>|<span data-ttu-id="86f6e-720">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-720">Required</span></span>|<span data-ttu-id="86f6e-721">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-721">Type</span></span>|<span data-ttu-id="86f6e-722">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-723">Azioni</span><span class="sxs-lookup"><span data-stu-id="86f6e-723">actions</span></span>|<span data-ttu-id="86f6e-724">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-724">Yes</span></span>|<span data-ttu-id="86f6e-725">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-725">Object</span></span>|<span data-ttu-id="86f6e-726">Azioni interne da eseguire nel ciclo</span><span class="sxs-lookup"><span data-stu-id="86f6e-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="86f6e-727">foreach</span><span class="sxs-lookup"><span data-stu-id="86f6e-727">foreach</span></span>|<span data-ttu-id="86f6e-728">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-728">Yes</span></span>|<span data-ttu-id="86f6e-729">string</span><span class="sxs-lookup"><span data-stu-id="86f6e-729">string</span></span>|<span data-ttu-id="86f6e-730">Matrice da scorrere</span><span class="sxs-lookup"><span data-stu-id="86f6e-730">The array to iterate over</span></span>|
|<span data-ttu-id="86f6e-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="86f6e-731">operationOptions</span></span>|<span data-ttu-id="86f6e-732">no</span><span class="sxs-lookup"><span data-stu-id="86f6e-732">no</span></span>|<span data-ttu-id="86f6e-733">string</span><span class="sxs-lookup"><span data-stu-id="86f6e-733">string</span></span>|<span data-ttu-id="86f6e-734">Qualsiasi opzione di operazione per il comportamento.</span><span class="sxs-lookup"><span data-stu-id="86f6e-734">Any operation options for behavior.</span></span> <span data-ttu-id="86f6e-735">Attualmente supporta solo `sequential` per eseguire le iterazioni in sequenza. Il comportamento predefinito è parallelo</span><span class="sxs-lookup"><span data-stu-id="86f6e-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="86f6e-736">Azione Until</span><span class="sxs-lookup"><span data-stu-id="86f6e-736">Until action</span></span>

<span data-ttu-id="86f6e-737">Questa azione di riproduzione a ciclo continuo esegue azioni interne finché una condizione non restituisce true.</span><span class="sxs-lookup"><span data-stu-id="86f6e-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="86f6e-738">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-738">Name</span></span>|<span data-ttu-id="86f6e-739">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-739">Required</span></span>|<span data-ttu-id="86f6e-740">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-740">Type</span></span>|<span data-ttu-id="86f6e-741">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-742">Azioni</span><span class="sxs-lookup"><span data-stu-id="86f6e-742">actions</span></span>|<span data-ttu-id="86f6e-743">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-743">Yes</span></span>|<span data-ttu-id="86f6e-744">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-744">Object</span></span>|<span data-ttu-id="86f6e-745">Azioni interne da eseguire nel ciclo</span><span class="sxs-lookup"><span data-stu-id="86f6e-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="86f6e-746">expression</span><span class="sxs-lookup"><span data-stu-id="86f6e-746">expression</span></span>|<span data-ttu-id="86f6e-747">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-747">Yes</span></span>|<span data-ttu-id="86f6e-748">string</span><span class="sxs-lookup"><span data-stu-id="86f6e-748">string</span></span>|<span data-ttu-id="86f6e-749">Espressione da valutare dopo ogni iterazione</span><span class="sxs-lookup"><span data-stu-id="86f6e-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="86f6e-750">limit</span><span class="sxs-lookup"><span data-stu-id="86f6e-750">limit</span></span>|<span data-ttu-id="86f6e-751">sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-751">yes</span></span>|<span data-ttu-id="86f6e-752">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-752">Object</span></span>|<span data-ttu-id="86f6e-753">Limiti per il ciclo: deve essere definito almeno un limite</span><span class="sxs-lookup"><span data-stu-id="86f6e-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="86f6e-754">count</span><span class="sxs-lookup"><span data-stu-id="86f6e-754">count</span></span>|<span data-ttu-id="86f6e-755">no</span><span class="sxs-lookup"><span data-stu-id="86f6e-755">no</span></span>|<span data-ttu-id="86f6e-756">int</span><span class="sxs-lookup"><span data-stu-id="86f6e-756">int</span></span>|<span data-ttu-id="86f6e-757">Limite per il numero di iterazioni che possono essere eseguite</span><span class="sxs-lookup"><span data-stu-id="86f6e-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="86f6e-758">timeout</span><span class="sxs-lookup"><span data-stu-id="86f6e-758">timeout</span></span>|<span data-ttu-id="86f6e-759">no</span><span class="sxs-lookup"><span data-stu-id="86f6e-759">no</span></span>|<span data-ttu-id="86f6e-760">string</span><span class="sxs-lookup"><span data-stu-id="86f6e-760">string</span></span>|<span data-ttu-id="86f6e-761">Timeout per la durata del ciclo.</span><span class="sxs-lookup"><span data-stu-id="86f6e-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="86f6e-762">Formato ISO 8601</span><span class="sxs-lookup"><span data-stu-id="86f6e-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="86f6e-763">Condizioni: azione If</span><span class="sxs-lookup"><span data-stu-id="86f6e-763">Conditions - If Action</span></span>

<span data-ttu-id="86f6e-764">L'azione `If` consente di valutare una condizione e di eseguire un ramo se l'espressione restituisce `true`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="86f6e-765">Nome</span><span class="sxs-lookup"><span data-stu-id="86f6e-765">Name</span></span>|<span data-ttu-id="86f6e-766">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="86f6e-766">Required</span></span>|<span data-ttu-id="86f6e-767">Tipo</span><span class="sxs-lookup"><span data-stu-id="86f6e-767">Type</span></span>|<span data-ttu-id="86f6e-768">Descrizione</span><span class="sxs-lookup"><span data-stu-id="86f6e-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="86f6e-769">Azioni</span><span class="sxs-lookup"><span data-stu-id="86f6e-769">actions</span></span>|<span data-ttu-id="86f6e-770">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-770">Yes</span></span>|<span data-ttu-id="86f6e-771">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-771">Object</span></span>|<span data-ttu-id="86f6e-772">Azioni interne da eseguire quando l'espressione restituisce `true`</span><span class="sxs-lookup"><span data-stu-id="86f6e-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="86f6e-773">expression</span><span class="sxs-lookup"><span data-stu-id="86f6e-773">expression</span></span>|<span data-ttu-id="86f6e-774">Sì</span><span class="sxs-lookup"><span data-stu-id="86f6e-774">Yes</span></span>|<span data-ttu-id="86f6e-775">string</span><span class="sxs-lookup"><span data-stu-id="86f6e-775">string</span></span>|<span data-ttu-id="86f6e-776">Espressione da valutare</span><span class="sxs-lookup"><span data-stu-id="86f6e-776">The expression to evaluate</span></span>|
|<span data-ttu-id="86f6e-777">else</span><span class="sxs-lookup"><span data-stu-id="86f6e-777">else</span></span>|<span data-ttu-id="86f6e-778">no</span><span class="sxs-lookup"><span data-stu-id="86f6e-778">no</span></span>|<span data-ttu-id="86f6e-779">Oggetto</span><span class="sxs-lookup"><span data-stu-id="86f6e-779">Object</span></span>|<span data-ttu-id="86f6e-780">Azioni interne da eseguire quando l'espressione restituisce `false`</span><span class="sxs-lookup"><span data-stu-id="86f6e-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="86f6e-781">La tabella seguente illustra alcuni esempi di come le condizioni possono usare le espressioni in un'azione:</span><span class="sxs-lookup"><span data-stu-id="86f6e-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="86f6e-782">Valore JSON</span><span class="sxs-lookup"><span data-stu-id="86f6e-782">JSON value</span></span>|<span data-ttu-id="86f6e-783">Risultato</span><span class="sxs-lookup"><span data-stu-id="86f6e-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="86f6e-784">Tutti i valori che restituiscono true fanno sì che questa condizione passi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="86f6e-785">Sono supportate solo le espressioni booleane.</span><span class="sxs-lookup"><span data-stu-id="86f6e-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="86f6e-786">Per convertire gli altri tipi in booleani, usare le funzioni `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="86f6e-787">Sono supportate le funzioni di confronto.</span><span class="sxs-lookup"><span data-stu-id="86f6e-787">Comparison functions are supported.</span></span> <span data-ttu-id="86f6e-788">In questo esempio l'azione viene eseguita solo quando l'output di act1 è maggiore della soglia.</span><span class="sxs-lookup"><span data-stu-id="86f6e-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="86f6e-789">Sono supportate anche le funzioni logiche per creare espressioni booleane annidate.</span><span class="sxs-lookup"><span data-stu-id="86f6e-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="86f6e-790">In questo caso, l'azione viene eseguita quando l'output di act1 è superiore alla soglia o inferiore a 100.</span><span class="sxs-lookup"><span data-stu-id="86f6e-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="86f6e-791">È possibile usare le funzioni di matrice per controllare se una matrice contiene elementi.</span><span class="sxs-lookup"><span data-stu-id="86f6e-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="86f6e-792">In questo caso, l'azione viene eseguita quando la matrice di errori è vuota.</span><span class="sxs-lookup"><span data-stu-id="86f6e-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="86f6e-793">Errore: condizione non valida perché @ è obbligatorio per le condizioni.</span><span class="sxs-lookup"><span data-stu-id="86f6e-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="86f6e-794">Se una condizione restituisce un valore corretto, viene contrassegnata come `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="86f6e-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="86f6e-795">Le azioni negli oggetti `actions` o `else` restituiscono `Succeeded` quando vengono eseguite correttamente, `Failed` quando non vengono eseguite correttamente o `Skipped` quando tale ramo non viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="86f6e-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86f6e-796">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86f6e-796">Next steps</span></span>

[<span data-ttu-id="86f6e-797">API REST del servizio flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="86f6e-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
