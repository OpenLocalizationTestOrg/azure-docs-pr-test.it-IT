---
title: aaaWorkflow azioni e trigger - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="eaf47-102">Azioni e trigger del flusso di lavoro per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="eaf47-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="eaf47-103">Le app per la logica sono costituite da trigger e da azioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="eaf47-104">Sono disponibili sei tipi di trigger.</span><span class="sxs-lookup"><span data-stu-id="eaf47-104">There are six types of triggers.</span></span> <span data-ttu-id="eaf47-105">Ogni tipo ha un'interfaccia e un comportamento diversi.</span><span class="sxs-lookup"><span data-stu-id="eaf47-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="eaf47-106">È inoltre possibile apprendere altri dettagli, esaminando i dettagli di hello di hello [il linguaggio di definizione del flusso di lavoro](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="eaf47-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="eaf47-107">Continuare a leggere toolearn ulteriori informazioni sui trigger e le azioni e come è possibile usarli toobuild logica App tooimprove i processi di business e flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="eaf47-108">Trigger</span><span class="sxs-lookup"><span data-stu-id="eaf47-108">Triggers</span></span>  

<span data-ttu-id="eaf47-109">Un trigger specifica chiamate hello in grado di avviare un'esecuzione del flusso di lavoro logica app.</span><span class="sxs-lookup"><span data-stu-id="eaf47-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="eaf47-110">Di seguito sono due modi diversi di hello tooinitiate un'esecuzione del flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="eaf47-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="eaf47-111">Un trigger di poll</span><span class="sxs-lookup"><span data-stu-id="eaf47-111">A polling trigger</span></span>  

-   <span data-ttu-id="eaf47-112">Un trigger di push - dal chiamante hello [API REST del servizio del flusso di lavoro](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="eaf47-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="eaf47-113">Tutti i trigger contengono questi elementi di livello superiore:</span><span class="sxs-lookup"><span data-stu-id="eaf47-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="eaf47-114">Tipi e input dei trigger</span><span class="sxs-lookup"><span data-stu-id="eaf47-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="eaf47-115">È possibile usare questi tipi di trigger:</span><span class="sxs-lookup"><span data-stu-id="eaf47-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="eaf47-116">**Richiesta** \- rende hello logica app un endpoint per è toocall</span><span class="sxs-lookup"><span data-stu-id="eaf47-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="eaf47-117">**Recurrence** \- Esegue l'attivazione in base a una pianificazione definita</span><span class="sxs-lookup"><span data-stu-id="eaf47-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="eaf47-118">**HTTP**\- Esegue il polling di un endpoint Web HTTP.</span><span class="sxs-lookup"><span data-stu-id="eaf47-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="eaf47-119">endpoint HTTP Hello devono essere conformi a contratto di attivazione specifica tooa \- utilizzando un codice 202\-un modello asincrono, oppure tramite la restituzione di una matrice</span><span class="sxs-lookup"><span data-stu-id="eaf47-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="eaf47-120">**ApiConnection** \- trigger viene eseguito il polling come hello HTTP, tuttavia, consente di usufruire di hello [API gestita da Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="eaf47-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="eaf47-121">**HTTPWebhook** \- viene aperto un endpoint, simile toohello manuale trigger, tuttavia, viene inoltre chiamato out tooa tooregister URL specificato e annullare la registrazione</span><span class="sxs-lookup"><span data-stu-id="eaf47-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="eaf47-122">**ApiConnectionWebhook** \- opera come hello trigger HTTPWebhook sfruttando hello API gestita da Microsoft</span><span class="sxs-lookup"><span data-stu-id="eaf47-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="eaf47-123">Ogni tipo di trigger ha un diverso set di **input** che ne definisce il comportamento.</span><span class="sxs-lookup"><span data-stu-id="eaf47-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="eaf47-124">Trigger di richiesta</span><span class="sxs-lookup"><span data-stu-id="eaf47-124">Request trigger</span></span>  

<span data-ttu-id="eaf47-125">Questo trigger opera come un endpoint che si chiamano tramite tooinvoke una richiesta HTTP app logica.</span><span class="sxs-lookup"><span data-stu-id="eaf47-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="eaf47-126">Un trigger request è simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="eaf47-127">Esiste anche una proprietà facoltativa denominata **schema**:</span><span class="sxs-lookup"><span data-stu-id="eaf47-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="eaf47-128">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-128">Element name</span></span>|<span data-ttu-id="eaf47-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eaf47-129">Required</span></span>|<span data-ttu-id="eaf47-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="eaf47-131">schema</span><span class="sxs-lookup"><span data-stu-id="eaf47-131">schema</span></span>|<span data-ttu-id="eaf47-132">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-132">No</span></span>|<span data-ttu-id="eaf47-133">Schema JSON che convalida la richiesta in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="eaf47-134">È utile per aiutare i passaggi successivi del flusso di lavoro sapere quali tooreference di proprietà.</span><span class="sxs-lookup"><span data-stu-id="eaf47-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="eaf47-135">tooinvoke questo endpoint, è necessario hello toocall *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="eaf47-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="eaf47-136">Vedere [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows) (API REST del servizio di flusso di lavoro).</span><span class="sxs-lookup"><span data-stu-id="eaf47-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="eaf47-137">Trigger Recurrence</span><span class="sxs-lookup"><span data-stu-id="eaf47-137">Recurrence trigger</span></span>  

<span data-ttu-id="eaf47-138">Un trigger Recurrence viene eseguito in base a una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="eaf47-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="eaf47-139">Tale trigger può essere simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="eaf47-140">Come si può notare, è toorun un modo semplice un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="eaf47-141">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-141">Element name</span></span>|<span data-ttu-id="eaf47-142">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eaf47-142">Required</span></span>|<span data-ttu-id="eaf47-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="eaf47-144">frequency</span><span class="sxs-lookup"><span data-stu-id="eaf47-144">frequency</span></span>|<span data-ttu-id="eaf47-145">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-145">Yes</span></span>|<span data-ttu-id="eaf47-146">La frequenza con cui hello trigger viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="eaf47-146">How often hello trigger executes.</span></span> <span data-ttu-id="eaf47-147">Usare solo uno di questi possibili valori: second, minute, hour, day, week, month o year</span><span class="sxs-lookup"><span data-stu-id="eaf47-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="eaf47-148">interval</span><span class="sxs-lookup"><span data-stu-id="eaf47-148">interval</span></span>|<span data-ttu-id="eaf47-149">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-149">Yes</span></span>|<span data-ttu-id="eaf47-150">Intervallo di hello dato frequenza ricorrenza hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="eaf47-151">startTime</span><span class="sxs-lookup"><span data-stu-id="eaf47-151">startTime</span></span>|<span data-ttu-id="eaf47-152">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-152">No</span></span>|<span data-ttu-id="eaf47-153">Se viene fornito un valore startTime senza una differenza dall'ora UTC, viene usato tale valore timeZone.</span><span class="sxs-lookup"><span data-stu-id="eaf47-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="eaf47-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="eaf47-154">timeZone</span></span>|<span data-ttu-id="eaf47-155">no</span><span class="sxs-lookup"><span data-stu-id="eaf47-155">no</span></span>|<span data-ttu-id="eaf47-156">Se viene fornito un valore startTime senza una differenza dall'ora UTC, viene usato tale valore timeZone.</span><span class="sxs-lookup"><span data-stu-id="eaf47-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="eaf47-157">È inoltre possibile pianificare un trigger toostart in esecuzione in un determinato hello future.</span><span class="sxs-lookup"><span data-stu-id="eaf47-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="eaf47-158">Ad esempio, se si desidera un riepilogo settimanale report ogni lunedì toostart è possibile pianificare hello logica app toostart come ogni lunedì, creando hello seguenti trigger:</span><span class="sxs-lookup"><span data-stu-id="eaf47-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="eaf47-159">Trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="eaf47-159">HTTP trigger</span></span>  

<span data-ttu-id="eaf47-160">I trigger HTTP il polling di un endpoint specificato e controllare hello risposta toodetermine se il flusso di lavoro hello deve essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="eaf47-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="eaf47-161">oggetto di input Hello prende il set di hello di parametri necessari tooconstruct una chiamata HTTP:</span><span class="sxs-lookup"><span data-stu-id="eaf47-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="eaf47-162">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-162">Element name</span></span>|<span data-ttu-id="eaf47-163">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eaf47-163">Required</span></span>|<span data-ttu-id="eaf47-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-164">Description</span></span>|<span data-ttu-id="eaf47-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="eaf47-166">statico</span><span class="sxs-lookup"><span data-stu-id="eaf47-166">method</span></span>|<span data-ttu-id="eaf47-167">sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-167">yes</span></span>|<span data-ttu-id="eaf47-168">Può essere uno dei seguenti metodi HTTP hello: GET, POST, PUT, DELETE, PATCH o HEAD</span><span class="sxs-lookup"><span data-stu-id="eaf47-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="eaf47-169">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-169">String</span></span>|  
|<span data-ttu-id="eaf47-170">Uri</span><span class="sxs-lookup"><span data-stu-id="eaf47-170">uri</span></span>|<span data-ttu-id="eaf47-171">sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-171">yes</span></span>|<span data-ttu-id="eaf47-172">Hello endpoint http o https che viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="eaf47-173">Il valore massimo è di 2 kilobyte.</span><span class="sxs-lookup"><span data-stu-id="eaf47-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="eaf47-174">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-174">String</span></span>|  
|<span data-ttu-id="eaf47-175">query</span><span class="sxs-lookup"><span data-stu-id="eaf47-175">queries</span></span>|<span data-ttu-id="eaf47-176">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-176">No</span></span>|<span data-ttu-id="eaf47-177">Oggetto che rappresenta hello query parametri tooadd toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="eaf47-178">Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="eaf47-179">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-179">Object</span></span>|  
|<span data-ttu-id="eaf47-180">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-180">headers</span></span>|<span data-ttu-id="eaf47-181">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-181">No</span></span>|<span data-ttu-id="eaf47-182">Oggetto che rappresenta ciascuna delle intestazioni di hello inviato toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="eaf47-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="eaf47-183">Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="eaf47-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="eaf47-184">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-184">Object</span></span>|  
|<span data-ttu-id="eaf47-185">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-185">body</span></span>|<span data-ttu-id="eaf47-186">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-186">No</span></span>|<span data-ttu-id="eaf47-187">Oggetto che rappresenta il payload hello inviato toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="eaf47-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="eaf47-188">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-188">Object</span></span>|  
|<span data-ttu-id="eaf47-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="eaf47-189">retryPolicy</span></span>|<span data-ttu-id="eaf47-190">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-190">No</span></span>|<span data-ttu-id="eaf47-191">Oggetto che consente di personalizzare il comportamento di ripetizione hello 4xx o 5xx errori.</span><span class="sxs-lookup"><span data-stu-id="eaf47-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="eaf47-192">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-192">Object</span></span>|  
|<span data-ttu-id="eaf47-193">authentication</span><span class="sxs-lookup"><span data-stu-id="eaf47-193">authentication</span></span>|<span data-ttu-id="eaf47-194">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-194">No</span></span>|<span data-ttu-id="eaf47-195">Metodo hello rappresenta hello richiesta deve essere autenticata.</span><span class="sxs-lookup"><span data-stu-id="eaf47-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="eaf47-196">Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="eaf47-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="eaf47-197">Oltre all'utilità di pianificazione, esiste un'altra proprietà supportata: `authority`. Per impostazione predefinita, questo valore è `https://login.windows.net` quando non viene specificato, ma è possibile usare un gruppo di destinatari diverso, ad esempio `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="eaf47-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="eaf47-198">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-198">Object</span></span>|  
  
<span data-ttu-id="eaf47-199">trigger di Hello HTTP richiede hello API HTTP tooconform con toowork un modello specifico e con l'app logica.</span><span class="sxs-lookup"><span data-stu-id="eaf47-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="eaf47-200">Richiede hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="eaf47-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="eaf47-201">Response</span><span class="sxs-lookup"><span data-stu-id="eaf47-201">Response</span></span>|<span data-ttu-id="eaf47-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="eaf47-203">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="eaf47-203">Status code</span></span>|<span data-ttu-id="eaf47-204">Codice di stato 200 \(OK\) toocause un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="eaf47-205">Nessun altro codice di stato attiva un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="eaf47-206">Intestazione Retry\-after</span><span class="sxs-lookup"><span data-stu-id="eaf47-206">Retry\-after header</span></span>|<span data-ttu-id="eaf47-207">Numero di secondi fino a quando non esegue il polling nuovamente hello logica app endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="eaf47-208">Intestazione Location</span><span class="sxs-lookup"><span data-stu-id="eaf47-208">Location header</span></span>|<span data-ttu-id="eaf47-209">intervallo di polling successivo hello, Hello toocall URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="eaf47-210">Se non specificato, viene utilizzato l'URL originale hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="eaf47-211">Di seguito sono riportati alcuni esempi di comportamenti diversi a seconda del tipo di richiesta:</span><span class="sxs-lookup"><span data-stu-id="eaf47-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="eaf47-212">Codice della risposta</span><span class="sxs-lookup"><span data-stu-id="eaf47-212">Response code</span></span>|<span data-ttu-id="eaf47-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="eaf47-213">Retry\-After</span></span>|<span data-ttu-id="eaf47-214">Comportamento</span><span class="sxs-lookup"><span data-stu-id="eaf47-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="eaf47-215">200</span><span class="sxs-lookup"><span data-stu-id="eaf47-215">200</span></span>|<span data-ttu-id="eaf47-216">\(nessuna\)</span><span class="sxs-lookup"><span data-stu-id="eaf47-216">\(none\)</span></span>|<span data-ttu-id="eaf47-217">Un trigger non valido, nuovo tentativo\-dopo il motore hello necessarie, altrimenti non esegue il polling per la richiesta successiva hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="eaf47-218">202</span><span class="sxs-lookup"><span data-stu-id="eaf47-218">202</span></span>|<span data-ttu-id="eaf47-219">60</span><span class="sxs-lookup"><span data-stu-id="eaf47-219">60</span></span>|<span data-ttu-id="eaf47-220">Flusso di lavoro hello non attivano.</span><span class="sxs-lookup"><span data-stu-id="eaf47-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="eaf47-221">viene eseguito il tentativo successivo di Hello in un minuto.</span><span class="sxs-lookup"><span data-stu-id="eaf47-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="eaf47-222">200</span><span class="sxs-lookup"><span data-stu-id="eaf47-222">200</span></span>|<span data-ttu-id="eaf47-223">10</span><span class="sxs-lookup"><span data-stu-id="eaf47-223">10</span></span>|<span data-ttu-id="eaf47-224">Esecuzione del flusso di lavoro hello e controllare di nuovo per il contenuto di più di 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="eaf47-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="eaf47-225">400</span><span class="sxs-lookup"><span data-stu-id="eaf47-225">400</span></span>|<span data-ttu-id="eaf47-226">\(nessuna\)</span><span class="sxs-lookup"><span data-stu-id="eaf47-226">\(none\)</span></span>|<span data-ttu-id="eaf47-227">Richiesta non valida, non eseguire il flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="eaf47-228">Se è presente alcun **criteri di ripetizione** definito, il criterio predefinito hello viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="eaf47-229">Una volta raggiunto il numero di hello tentativi, il trigger di hello non è più valido.</span><span class="sxs-lookup"><span data-stu-id="eaf47-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="eaf47-230">500</span><span class="sxs-lookup"><span data-stu-id="eaf47-230">500</span></span>|<span data-ttu-id="eaf47-231">\(nessuna\)</span><span class="sxs-lookup"><span data-stu-id="eaf47-231">\(none\)</span></span>|<span data-ttu-id="eaf47-232">Errore del server, non sono in esecuzione del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="eaf47-233">Se è presente alcun **criteri di ripetizione** definito, il criterio predefinito hello viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="eaf47-234">Una volta raggiunto il numero di hello tentativi, il trigger di hello non è più valido.</span><span class="sxs-lookup"><span data-stu-id="eaf47-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="eaf47-235">output di Hello di un trigger HTTP aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf47-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="eaf47-236">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-236">Element name</span></span>|<span data-ttu-id="eaf47-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-237">Description</span></span>|<span data-ttu-id="eaf47-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="eaf47-239">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-239">headers</span></span>|<span data-ttu-id="eaf47-240">intestazioni Hello di risposta http hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-240">hello headers of hello http response.</span></span>|<span data-ttu-id="eaf47-241">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-241">Object</span></span>|  
|<span data-ttu-id="eaf47-242">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-242">body</span></span>|<span data-ttu-id="eaf47-243">corpo Hello di risposta http hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-243">hello body of hello http response.</span></span>|<span data-ttu-id="eaf47-244">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="eaf47-245">Trigger ApiConnection</span><span class="sxs-lookup"><span data-stu-id="eaf47-245">API Connection trigger</span></span>  

<span data-ttu-id="eaf47-246">Hello API connessione tratta simile toohello HTTP trigger nella funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="eaf47-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="eaf47-247">Tuttavia, i parametri di hello per identificare l'azione di hello sono diversi.</span><span class="sxs-lookup"><span data-stu-id="eaf47-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="eaf47-248">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="eaf47-249">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-249">Element name</span></span>|<span data-ttu-id="eaf47-250">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-250">Required</span></span>|<span data-ttu-id="eaf47-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-251">Type</span></span>|<span data-ttu-id="eaf47-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-253">host</span><span class="sxs-lookup"><span data-stu-id="eaf47-253">host</span></span>|<span data-ttu-id="eaf47-254">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-254">Yes</span></span>||<span data-ttu-id="eaf47-255">Hello ApiApp host gateway e id.</span><span class="sxs-lookup"><span data-stu-id="eaf47-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="eaf47-256">statico</span><span class="sxs-lookup"><span data-stu-id="eaf47-256">method</span></span>|<span data-ttu-id="eaf47-257">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-257">Yes</span></span>|<span data-ttu-id="eaf47-258">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-258">String</span></span>|<span data-ttu-id="eaf47-259">Può essere uno dei seguenti metodi HTTP hello: **ottenere**, **POST**, **inserire**, **eliminare**, **PATCH**, o  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="eaf47-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="eaf47-260">query</span><span class="sxs-lookup"><span data-stu-id="eaf47-260">queries</span></span>|<span data-ttu-id="eaf47-261">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-261">No</span></span>|<span data-ttu-id="eaf47-262">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-262">Object</span></span>|<span data-ttu-id="eaf47-263">Rappresenta hello query parametri toobe aggiunto toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="eaf47-264">Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="eaf47-265">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-265">headers</span></span>|<span data-ttu-id="eaf47-266">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-266">No</span></span>|<span data-ttu-id="eaf47-267">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-267">Object</span></span>|<span data-ttu-id="eaf47-268">Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di.</span><span class="sxs-lookup"><span data-stu-id="eaf47-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="eaf47-269">Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="eaf47-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="eaf47-270">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-270">body</span></span>|<span data-ttu-id="eaf47-271">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-271">No</span></span>|<span data-ttu-id="eaf47-272">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-272">Object</span></span>|<span data-ttu-id="eaf47-273">Rappresenta il payload hello inviato toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="eaf47-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="eaf47-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="eaf47-274">retryPolicy</span></span>|<span data-ttu-id="eaf47-275">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-275">No</span></span>|<span data-ttu-id="eaf47-276">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-276">Object</span></span>|<span data-ttu-id="eaf47-277">Consente di comportamento del nuovo tentativo hello toocustomize 4xx o 5xx errori.</span><span class="sxs-lookup"><span data-stu-id="eaf47-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="eaf47-278">authentication</span><span class="sxs-lookup"><span data-stu-id="eaf47-278">authentication</span></span>|<span data-ttu-id="eaf47-279">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-279">No</span></span>|<span data-ttu-id="eaf47-280">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-280">Object</span></span>|<span data-ttu-id="eaf47-281">Metodo hello rappresenta hello richiesta deve essere autenticata.</span><span class="sxs-lookup"><span data-stu-id="eaf47-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="eaf47-282">Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="eaf47-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="eaf47-283">proprietà Hello per host sono:</span><span class="sxs-lookup"><span data-stu-id="eaf47-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="eaf47-284">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-284">Element name</span></span>|<span data-ttu-id="eaf47-285">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eaf47-285">Required</span></span>|<span data-ttu-id="eaf47-286">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="eaf47-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="eaf47-287">api runtimeUrl</span></span>|<span data-ttu-id="eaf47-288">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-288">Yes</span></span>|<span data-ttu-id="eaf47-289">endpoint Hello di hello API gestita.</span><span class="sxs-lookup"><span data-stu-id="eaf47-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="eaf47-290">connection name</span><span class="sxs-lookup"><span data-stu-id="eaf47-290">connection name</span></span>||<span data-ttu-id="eaf47-291">Deve essere un parametro di riferimento tooa chiamato `$connection` ed è il nome di hello della connessione di API gestita hello che hello del flusso di lavoro viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="eaf47-292">output di Hello di un trigger di connessione API sono:</span><span class="sxs-lookup"><span data-stu-id="eaf47-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="eaf47-293">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-293">Element name</span></span>|<span data-ttu-id="eaf47-294">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-294">Type</span></span>|<span data-ttu-id="eaf47-295">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="eaf47-296">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-296">headers</span></span>|<span data-ttu-id="eaf47-297">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-297">Object</span></span>|<span data-ttu-id="eaf47-298">intestazioni Hello di risposta http hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="eaf47-299">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-299">body</span></span>|<span data-ttu-id="eaf47-300">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-300">Object</span></span>|<span data-ttu-id="eaf47-301">corpo Hello di risposta http hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="eaf47-302">Trigger HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="eaf47-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="eaf47-303">verrà visualizzata la trigger HTTPWebhook Hello un endpoint, i trigger manuale di toohello simile, ma hello trigger HTTPWebhook anche effettua una chiamata tooa tooregister URL specificato e annullare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="eaf47-304">Ecco un esempio di come si presenta un trigger HTTPWebhook:</span><span class="sxs-lookup"><span data-stu-id="eaf47-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="eaf47-305">Molte di queste sezioni sono facoltativi e il comportamento di hello di hello Webhook dipende da quali sezioni sono fornite o omesso.</span><span class="sxs-lookup"><span data-stu-id="eaf47-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="eaf47-306">proprietà Hello di un Webhook sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaf47-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="eaf47-307">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-307">Element name</span></span>|<span data-ttu-id="eaf47-308">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eaf47-308">Required</span></span>|<span data-ttu-id="eaf47-309">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="eaf47-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="eaf47-310">subscribe</span></span>|<span data-ttu-id="eaf47-311">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-311">No</span></span>|<span data-ttu-id="eaf47-312">Hello in uscita richiesta che viene chiamato quando il trigger di hello viene creato ed esegue la registrazione iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="eaf47-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="eaf47-313">unsubscribe</span></span>|<span data-ttu-id="eaf47-314">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-314">No</span></span>|<span data-ttu-id="eaf47-315">Hello in uscita richiesta quando viene eliminato il trigger di hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="eaf47-316">**La sottoscrizione** è hello chiamata che ha apportato tooevents ascolto toostart in uscita.</span><span class="sxs-lookup"><span data-stu-id="eaf47-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="eaf47-317">Questa chiamata inizia con hello si stesso set di parametri che hello azioni HTTP normale.</span><span class="sxs-lookup"><span data-stu-id="eaf47-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="eaf47-318">Questa chiamata in uscita viene eseguita qualsiasi hello ora le modifiche del flusso di lavoro in qualsiasi modo, ad esempio, ogni volta che le credenziali di hello vengono eseguito il rollback o modifica i parametri di input del trigger hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="eaf47-319">toosupport questa chiamata è una nuova funzione: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="eaf47-320">Questa funzione restituisce un URL univoco per il trigger specifico nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="eaf47-321">Rappresenta l'identificatore univoco di hello per gli endpoint di hello che utilizzano hello servizio REST.</span><span class="sxs-lookup"><span data-stu-id="eaf47-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="eaf47-322">**Unsubscribe** viene chiamata quando un'operazione rende questo trigger non valido, tra cui:</span><span class="sxs-lookup"><span data-stu-id="eaf47-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="eaf47-323">L'eliminazione o la disabilitazione di trigger hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="eaf47-324">L'eliminazione o la disabilitazione del flusso di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="eaf47-325">L'eliminazione o la disabilitazione di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="eaf47-326">app per la logica Hello chiama automaticamente hello annullare l'azione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="eaf47-327">Hello parametri di funzione toothis hello stesso come trigger HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="eaf47-328">Hello output di trigger HTTPWebhook hello sono hello contenuto della richiesta in ingresso hello:</span><span class="sxs-lookup"><span data-stu-id="eaf47-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="eaf47-329">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-329">Element name</span></span>|<span data-ttu-id="eaf47-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-330">Type</span></span>|<span data-ttu-id="eaf47-331">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="eaf47-332">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-332">headers</span></span>|<span data-ttu-id="eaf47-333">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-333">Object</span></span>|<span data-ttu-id="eaf47-334">intestazioni Hello della richiesta http hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="eaf47-335">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-335">body</span></span>|<span data-ttu-id="eaf47-336">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-336">Object</span></span>|<span data-ttu-id="eaf47-337">corpo Hello della richiesta http hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="eaf47-338">È possibile specificare i limiti per un'azione di webhook in hello esattamente come [HTTP asincroni limiti](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="eaf47-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="eaf47-339">Condizioni</span><span class="sxs-lookup"><span data-stu-id="eaf47-339">Conditions</span></span>  

<span data-ttu-id="eaf47-340">Per qualsiasi trigger, è possibile utilizzare uno o più toodetermine condizioni se il flusso di lavoro hello deve essere eseguito o non.</span><span class="sxs-lookup"><span data-stu-id="eaf47-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="eaf47-341">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-341">For example:</span></span>  

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

<span data-ttu-id="eaf47-342">In questo caso, hello solo i trigger report durante il flusso di lavoro hello `sendReports` parametro è impostato tootrue.</span><span class="sxs-lookup"><span data-stu-id="eaf47-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="eaf47-343">Infine, le condizioni possono fare riferimento a codice di stato hello del trigger hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="eaf47-344">È possibile, ad esempio, avviare un flusso di lavoro solo quando il sito Web restituisce un codice di stato 500, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="eaf47-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="eaf47-345">Quando un'espressione fa riferimento a codice di stato hello del trigger hello \(in alcun modo\), hello comportamento predefinito \(trigger solo su 200 \(OK\) \) viene sostituito.</span><span class="sxs-lookup"><span data-stu-id="eaf47-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="eaf47-346">Ad esempio, se si desidera tootrigger sul codice di stato 200 sia il codice di stato 201, avere tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` come condizione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="eaf47-347">Avviare più esecuzioni per una richiesta</span><span class="sxs-lookup"><span data-stu-id="eaf47-347">Start multiple runs for a request</span></span>

<span data-ttu-id="eaf47-348">tookick esterno viene eseguito più volte per una singola richiesta, `splitOn` è utile, ad esempio, quando si desidera toopoll un endpoint che può avere più nuovi elementi tra gli intervalli di polling.</span><span class="sxs-lookup"><span data-stu-id="eaf47-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="eaf47-349">Con `splitOn`, si specifica la proprietà hello interno hello payload di risposta che contiene la matrice hello degli elementi, ognuno dei quali si vuole toouse toostart un'esecuzione di trigger hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="eaf47-350">Si supponga, ad esempio, che è disponibile un'API che restituisce hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="eaf47-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="eaf47-351">L'app di logica deve solo contenuto righe hello, pertanto è possibile creare il trigger come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="eaf47-352">Quindi, nella definizione di flusso di lavoro, hello `@triggerBody().name` restituisce `mycoolrow` per la prima esecuzione, hello e `another row` per la seconda esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="eaf47-353">Hello trigger output aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf47-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="eaf47-354">Pertanto, se si utilizza `SplitOn`, non è possibile ottenere le proprietà di hello che non rientrano hello matrice, in questo caso, hello `Status` campo.</span><span class="sxs-lookup"><span data-stu-id="eaf47-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="eaf47-355">In questo esempio, si usa hello `?` tooavoid in grado di operatore toobe un errore se hello `Rows` proprietà non è presente.</span><span class="sxs-lookup"><span data-stu-id="eaf47-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="eaf47-356">Istanza di esecuzione singola</span><span class="sxs-lookup"><span data-stu-id="eaf47-356">Single run instance</span></span>

<span data-ttu-id="eaf47-357">È possibile configurare i trigger che hanno un incendio tooonly di proprietà ricorrenza se sono state completate tutte le esecuzioni attive.</span><span class="sxs-lookup"><span data-stu-id="eaf47-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="eaf47-358">Se una ricorrenza pianificata si verifica mentre è presente un'esecuzione in corso, trigger hello Ignora e attende fino a quando hello successivo pianificato ricorrenza intervallo toocheck nuovamente.</span><span class="sxs-lookup"><span data-stu-id="eaf47-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="eaf47-359">È possibile configurare questa impostazione tramite le opzioni di operazione hello:</span><span class="sxs-lookup"><span data-stu-id="eaf47-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="eaf47-360">Tipi e input</span><span class="sxs-lookup"><span data-stu-id="eaf47-360">Types and inputs</span></span>  

<span data-ttu-id="eaf47-361">Esistono molti tipi di azioni, ognuna con un comportamento univoco.</span><span class="sxs-lookup"><span data-stu-id="eaf47-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="eaf47-362">Le azioni di raccolta possono contenere diverse altre azioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="eaf47-363">Azioni standard</span><span class="sxs-lookup"><span data-stu-id="eaf47-363">Standard actions</span></span>  

-   <span data-ttu-id="eaf47-364">**HTTP** Questa azione chiama un endpoint Web HTTP.</span><span class="sxs-lookup"><span data-stu-id="eaf47-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="eaf47-365">**ApiConnection** \- questa azione si comporta come hello azione HTTP, ma utilizza hello API gestita da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eaf47-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="eaf47-366">**ApiConnectionWebhook** \- HTTPWebhook simile, ma utilizza hello API gestita da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eaf47-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="eaf47-367">**Response** \- Questa azione definisce una risposta per una chiamata in ingresso.</span><span class="sxs-lookup"><span data-stu-id="eaf47-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="eaf47-368">**Wait** \- Questa semplice azione attende per un intervallo di tempo fisso o fino a un'ora specifica.</span><span class="sxs-lookup"><span data-stu-id="eaf47-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="eaf47-369">**Workflow**\- Questa azione rappresenta un flusso di lavoro annidato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="eaf47-370">**Function**\- Questa azione rappresenta una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf47-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="eaf47-371">Azioni di raccolta</span><span class="sxs-lookup"><span data-stu-id="eaf47-371">Collection actions</span></span>

-   <span data-ttu-id="eaf47-372">**Scope** \- Questa azione è un raggruppamento logico di altre azioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="eaf47-373">**Condizione** \- questa azione viene valutata un'espressione ed esegue il ramo risultato corrispondente di hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="eaf47-374">**ForEach** \- Questa azione di riproduzione a ciclo continuo scorre una matrice ed esegue azioni interne per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="eaf47-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="eaf47-375">**Fino a quando non** \- ciclo verrà eseguito azioni interne fino a quando una condizione risultati tootrue.</span><span class="sxs-lookup"><span data-stu-id="eaf47-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="eaf47-376">Ogni tipo di azione ha un set diverso di **input** che definiscono il comportamento di un'azione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="eaf47-377">Azione HTTP</span><span class="sxs-lookup"><span data-stu-id="eaf47-377">HTTP action</span></span>  

<span data-ttu-id="eaf47-378">Azioni HTTP chiamano un endpoint specificato e verificare hello risposta toodetermine se hello flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="eaf47-379">Hello **input** oggetto prende il set di hello di parametri necessari tooconstruct hello HTTP chiamata:</span><span class="sxs-lookup"><span data-stu-id="eaf47-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="eaf47-380">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-380">Element name</span></span>|<span data-ttu-id="eaf47-381">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-381">Required</span></span>|<span data-ttu-id="eaf47-382">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-382">Type</span></span>|<span data-ttu-id="eaf47-383">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-384">statico</span><span class="sxs-lookup"><span data-stu-id="eaf47-384">method</span></span>|<span data-ttu-id="eaf47-385">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-385">Yes</span></span>|<span data-ttu-id="eaf47-386">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-386">String</span></span>|<span data-ttu-id="eaf47-387">Può essere uno dei seguenti metodi HTTP hello: **ottenere**, **POST**, **inserire**, **eliminare**, **PATCH**, o  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="eaf47-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="eaf47-388">Uri</span><span class="sxs-lookup"><span data-stu-id="eaf47-388">uri</span></span>|<span data-ttu-id="eaf47-389">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-389">Yes</span></span>|<span data-ttu-id="eaf47-390">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-390">String</span></span>|<span data-ttu-id="eaf47-391">Hello endpoint http o https che viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="eaf47-392">La lunghezza massima è 2 kilobyte.</span><span class="sxs-lookup"><span data-stu-id="eaf47-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="eaf47-393">query</span><span class="sxs-lookup"><span data-stu-id="eaf47-393">queries</span></span>|<span data-ttu-id="eaf47-394">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-394">No</span></span>|<span data-ttu-id="eaf47-395">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-395">Object</span></span>|<span data-ttu-id="eaf47-396">Rappresenta l'URL toohello tooadd i parametri della query hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="eaf47-397">Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="eaf47-398">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-398">headers</span></span>|<span data-ttu-id="eaf47-399">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-399">No</span></span>|<span data-ttu-id="eaf47-400">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-400">Object</span></span>|<span data-ttu-id="eaf47-401">Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di.</span><span class="sxs-lookup"><span data-stu-id="eaf47-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="eaf47-402">Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="eaf47-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="eaf47-403">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-403">body</span></span>|<span data-ttu-id="eaf47-404">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-404">No</span></span>|<span data-ttu-id="eaf47-405">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-405">Object</span></span>|<span data-ttu-id="eaf47-406">Rappresenta il payload hello inviato toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="eaf47-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="eaf47-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="eaf47-407">retryPolicy</span></span>|<span data-ttu-id="eaf47-408">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-408">No</span></span>|<span data-ttu-id="eaf47-409">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-409">Object</span></span>|<span data-ttu-id="eaf47-410">Consente di personalizzare il comportamento di ripetizione hello 4xx o 5xx errori.</span><span class="sxs-lookup"><span data-stu-id="eaf47-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="eaf47-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="eaf47-411">operationsOptions</span></span>|<span data-ttu-id="eaf47-412">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-412">No</span></span>|<span data-ttu-id="eaf47-413">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-413">String</span></span>|<span data-ttu-id="eaf47-414">Definisce il set di hello di toooverride comportamenti speciali.</span><span class="sxs-lookup"><span data-stu-id="eaf47-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="eaf47-415">authentication</span><span class="sxs-lookup"><span data-stu-id="eaf47-415">authentication</span></span>|<span data-ttu-id="eaf47-416">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-416">No</span></span>|<span data-ttu-id="eaf47-417">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-417">Object</span></span>|<span data-ttu-id="eaf47-418">Metodo hello rappresenta hello richiesta deve essere autenticata.</span><span class="sxs-lookup"><span data-stu-id="eaf47-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="eaf47-419">Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="eaf47-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="eaf47-420">Oltre all'utilità di pianificazione, esiste un'altra proprietà supportata, `authority`,</span><span class="sxs-lookup"><span data-stu-id="eaf47-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="eaf47-421">che, per impostazione predefinita, è `https://login.windows.net` quando non è specificata, ma è possibile usare un gruppo di destinatari diverso, ad esempio `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="eaf47-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="eaf47-422">Le azioni HTTP \(e di connessione API\) supportano i criteri per i tentativi.</span><span class="sxs-lookup"><span data-stu-id="eaf47-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="eaf47-423">Un criterio di ripetizione applica toointermittent errori caratterizzati allo stato HTTP 408 429 e 5xx, eccezioni di connettività tooany inoltre i codici.</span><span class="sxs-lookup"><span data-stu-id="eaf47-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="eaf47-424">Questo criterio è descritto l'utilizzo di hello *retryPolicy* oggetto definito come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="eaf47-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="eaf47-425">intervallo tra tentativi Hello è specificato in formato ISO 8601 hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="eaf47-426">Questo intervallo ha un valore predefinito e il valore minimo di 20 secondi, mentre il valore massimo hello è un'ora.</span><span class="sxs-lookup"><span data-stu-id="eaf47-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="eaf47-427">numero di tentativi predefinito e massimo Hello corrisponde a quattro ore.</span><span class="sxs-lookup"><span data-stu-id="eaf47-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="eaf47-428">Se non viene specificata definizione dei criteri di ripetizione hello, un `fixed` strategia viene utilizzata con valori di conteggio e l'intervallo di tentativi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="eaf47-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="eaf47-429">criteri di ripetizione hello toodisable, impostare il relativo tipo troppo`None`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="eaf47-430">Ad esempio, hello azione seguente Ritenta recupero hello ultime notizie su due volte, se si sono verificati errori intermittenti, per un totale di tre esecuzioni, con un ritardo di 30 secondi tra ogni tentativo di:</span><span class="sxs-lookup"><span data-stu-id="eaf47-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="eaf47-431">Modelli asincroni</span><span class="sxs-lookup"><span data-stu-id="eaf47-431">Asynchronous patterns</span></span>

<span data-ttu-id="eaf47-432">Per impostazione predefinita, tutte le azioni basate su HTTP supportano il pattern di operazione asincrona standard hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="eaf47-433">Pertanto se il server remoto hello indica che la richiesta hello è accettato per l'elaborazione con un codice 202 \(accettato\) risposta, il motore di App per la logica hello mantiene polling specificato nell'intestazione location della risposta hello fino a raggiungere un terminale dell'URL di hello stato \(non\-risposta 202\).</span><span class="sxs-lookup"><span data-stu-id="eaf47-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="eaf47-434">comportamento asincrono di toodisable hello precedentemente descritto, imposta un `DisableAsyncPattern` opzione nell'input azione hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="eaf47-435">In questo caso, output di hello dell'azione hello dipende hello iniziale 202 risposta hello server.</span><span class="sxs-lookup"><span data-stu-id="eaf47-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="eaf47-436">Limiti asincroni</span><span class="sxs-lookup"><span data-stu-id="eaf47-436">Asynchronous Limits</span></span>

<span data-ttu-id="eaf47-437">Un modello asincrono può essere limitato nel relativo intervallo di tempo specifico tooa durata.</span><span class="sxs-lookup"><span data-stu-id="eaf47-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="eaf47-438">Allo scadere dell'intervallo di tempo hello non abbia raggiunto uno stato terminale, lo stato di hello dell'azione hello verrà contrassegnato `Cancelled` con codice `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="eaf47-439">timeout di limite Hello è specificato in formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="eaf47-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="eaf47-440">È possibile specificare limiti con hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="eaf47-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="eaf47-441">Connessione API</span><span class="sxs-lookup"><span data-stu-id="eaf47-441">API Connection</span></span>  

<span data-ttu-id="eaf47-442">La connessione API è un'azione che fa riferimento a un connettore gestito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eaf47-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="eaf47-443">Questa azione richiede una connessione valida tooa di riferimento e per informazioni sull'API hello e i parametri richiesti.</span><span class="sxs-lookup"><span data-stu-id="eaf47-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="eaf47-444">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="eaf47-444">Element name</span></span>|<span data-ttu-id="eaf47-445">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-445">Required</span></span>|<span data-ttu-id="eaf47-446">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-446">Type</span></span>|<span data-ttu-id="eaf47-447">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-448">host</span><span class="sxs-lookup"><span data-stu-id="eaf47-448">host</span></span>|<span data-ttu-id="eaf47-449">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-449">Yes</span></span>|<span data-ttu-id="eaf47-450">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-450">Object</span></span>|<span data-ttu-id="eaf47-451">Rappresenta informazioni sul connettore hello, ad esempio hello runtimeUrl e riferimento toohello oggetto di connessione</span><span class="sxs-lookup"><span data-stu-id="eaf47-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="eaf47-452">statico</span><span class="sxs-lookup"><span data-stu-id="eaf47-452">method</span></span>|<span data-ttu-id="eaf47-453">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-453">Yes</span></span>|<span data-ttu-id="eaf47-454">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-454">String</span></span>|<span data-ttu-id="eaf47-455">Può essere uno dei seguenti metodi HTTP hello: **ottenere**, **POST**, **inserire**, **eliminare**, **PATCH**, o  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="eaf47-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="eaf47-456">path</span><span class="sxs-lookup"><span data-stu-id="eaf47-456">path</span></span>|<span data-ttu-id="eaf47-457">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-457">Yes</span></span>|<span data-ttu-id="eaf47-458">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-458">String</span></span>|<span data-ttu-id="eaf47-459">percorso di Hello dell'operazione hello API.</span><span class="sxs-lookup"><span data-stu-id="eaf47-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="eaf47-460">query</span><span class="sxs-lookup"><span data-stu-id="eaf47-460">queries</span></span>|<span data-ttu-id="eaf47-461">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-461">No</span></span>|<span data-ttu-id="eaf47-462">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-462">Object</span></span>|<span data-ttu-id="eaf47-463">Rappresenta l'URL toohello tooadd i parametri della query hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="eaf47-464">Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="eaf47-465">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-465">headers</span></span>|<span data-ttu-id="eaf47-466">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-466">No</span></span>|<span data-ttu-id="eaf47-467">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-467">Object</span></span>|<span data-ttu-id="eaf47-468">Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di.</span><span class="sxs-lookup"><span data-stu-id="eaf47-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="eaf47-469">Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="eaf47-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="eaf47-470">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-470">body</span></span>|<span data-ttu-id="eaf47-471">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-471">No</span></span>|<span data-ttu-id="eaf47-472">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-472">Object</span></span>|<span data-ttu-id="eaf47-473">Rappresenta il payload hello inviato toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="eaf47-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="eaf47-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="eaf47-474">retryPolicy</span></span>|<span data-ttu-id="eaf47-475">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-475">No</span></span>|<span data-ttu-id="eaf47-476">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-476">Object</span></span>|<span data-ttu-id="eaf47-477">Consente di personalizzare il comportamento di ripetizione hello 4xx o 5xx errori.</span><span class="sxs-lookup"><span data-stu-id="eaf47-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="eaf47-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="eaf47-478">operationsOptions</span></span>|<span data-ttu-id="eaf47-479">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-479">No</span></span>|<span data-ttu-id="eaf47-480">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-480">String</span></span>|<span data-ttu-id="eaf47-481">Definisce il set di hello di toooverride comportamenti speciali.</span><span class="sxs-lookup"><span data-stu-id="eaf47-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="eaf47-482">Azione webhook di connessione API</span><span class="sxs-lookup"><span data-stu-id="eaf47-482">API Connection webhook action</span></span>

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

<span data-ttu-id="eaf47-483">È possibile specificare i limiti per un'azione di webhook in hello esattamente come [HTTP asincroni limiti](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="eaf47-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="eaf47-484">Azione di risposta</span><span class="sxs-lookup"><span data-stu-id="eaf47-484">Response action</span></span>  

<span data-ttu-id="eaf47-485">Questo tipo di azione contiene il payload della risposta hello da una richiesta HTTP e include un codice di stato, corpo e intestazioni:</span><span class="sxs-lookup"><span data-stu-id="eaf47-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="eaf47-486">azione di risposta Hello presenta restrizioni speciali che non si applicano tooother azioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="eaf47-487">In particolare:</span><span class="sxs-lookup"><span data-stu-id="eaf47-487">Specifically:</span></span>  
  
-   <span data-ttu-id="eaf47-488">Azioni di risposta non possono essere parallele in una definizione perché è necessaria una richiesta in ingresso toohello di risposta deterministica.</span><span class="sxs-lookup"><span data-stu-id="eaf47-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="eaf47-489">Se un'azione di risposta viene raggiunto dopo la richiesta in ingresso hello ha ricevuto una risposta, azione hello viene considerato non riuscito \(conflitto\), e di conseguenza, hello eseguire `Failed`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="eaf47-490">Un flusso di lavoro con azioni response non può avere `splitOn` nel trigger perché una chiamata genera più esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="eaf47-491">Di conseguenza, si devono essere convalidato quando il flusso di hello è PUT e causa una richiesta non valida.</span><span class="sxs-lookup"><span data-stu-id="eaf47-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="eaf47-492">Azione wait</span><span class="sxs-lookup"><span data-stu-id="eaf47-492">Wait action</span></span>  

<span data-ttu-id="eaf47-493">Hello `wait` azione sospende l'esecuzione del flusso di lavoro per l'intervallo specificato "hello".</span><span class="sxs-lookup"><span data-stu-id="eaf47-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="eaf47-494">Ad esempio, toowait 15 minuti, è possibile utilizzare questo frammento di codice:</span><span class="sxs-lookup"><span data-stu-id="eaf47-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="eaf47-495">In alternativa, toowait fino a un momento specifico, è possibile usare questo esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="eaf47-496">durata dell'attesa Hello può essere specificata sia utilizzando hello **intervallo** oggetto o hello **fino a quando non** oggetto, ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="eaf47-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="eaf47-497">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-497">Name</span></span>|<span data-ttu-id="eaf47-498">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-498">Required</span></span>|<span data-ttu-id="eaf47-499">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-499">Type</span></span>|<span data-ttu-id="eaf47-500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-501">interval</span><span class="sxs-lookup"><span data-stu-id="eaf47-501">interval</span></span>|<span data-ttu-id="eaf47-502">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-502">No</span></span>|<span data-ttu-id="eaf47-503">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-503">Object</span></span>|<span data-ttu-id="eaf47-504">Hello in base alle quantità di tempo di durata dell'attesa.</span><span class="sxs-lookup"><span data-stu-id="eaf47-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="eaf47-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="eaf47-505">interval unit</span></span>|<span data-ttu-id="eaf47-506">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-506">Yes</span></span>|<span data-ttu-id="eaf47-507">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-507">String</span></span>|<span data-ttu-id="eaf47-508">Uno di questi intervalli: second, minute, hour, day, week, month, year.</span><span class="sxs-lookup"><span data-stu-id="eaf47-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="eaf47-509">interval count</span><span class="sxs-lookup"><span data-stu-id="eaf47-509">interval count</span></span>|<span data-ttu-id="eaf47-510">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-510">Yes</span></span>|<span data-ttu-id="eaf47-511">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-511">String</span></span>|<span data-ttu-id="eaf47-512">Durata in base alle unità di misura interno determinata hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="eaf47-513">until</span><span class="sxs-lookup"><span data-stu-id="eaf47-513">until</span></span>|<span data-ttu-id="eaf47-514">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-514">No</span></span>|<span data-ttu-id="eaf47-515">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-515">Object</span></span>|<span data-ttu-id="eaf47-516">Hello basata su un punto nel tempo di durata dell'attesa.</span><span class="sxs-lookup"><span data-stu-id="eaf47-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="eaf47-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="eaf47-517">until timestamp</span></span>|<span data-ttu-id="eaf47-518">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-518">Yes</span></span>|<span data-ttu-id="eaf47-519">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-519">String</span></span>|<span data-ttu-id="eaf47-520">Stringa &#124; hello punto nel tempo in formato UTC quando hello attesa scade.</span><span class="sxs-lookup"><span data-stu-id="eaf47-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="eaf47-521">Azione di query</span><span class="sxs-lookup"><span data-stu-id="eaf47-521">Query action</span></span>

<span data-ttu-id="eaf47-522">Hello `query` azione consente di filtrare una matrice in base a una condizione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="eaf47-523">Ad esempio, tooselect numeri maggiori di 2, è possibile utilizzare:</span><span class="sxs-lookup"><span data-stu-id="eaf47-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="eaf47-524">output di hello Hello `query` azione è una matrice contenente gli elementi dalla matrice di input hello che soddisfano la condizione hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf47-525">Se nessun valore soddisfano hello `where` condizione, risultato hello è una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="eaf47-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="eaf47-526">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-526">Name</span></span>|<span data-ttu-id="eaf47-527">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-527">Required</span></span>|<span data-ttu-id="eaf47-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-528">Type</span></span>|<span data-ttu-id="eaf47-529">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="eaf47-530">from</span><span class="sxs-lookup"><span data-stu-id="eaf47-530">from</span></span>|<span data-ttu-id="eaf47-531">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-531">Yes</span></span>|<span data-ttu-id="eaf47-532">Array</span><span class="sxs-lookup"><span data-stu-id="eaf47-532">Array</span></span>|<span data-ttu-id="eaf47-533">Matrice di origine Hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-533">hello source array.</span></span>|
|<span data-ttu-id="eaf47-534">dove</span><span class="sxs-lookup"><span data-stu-id="eaf47-534">where</span></span>|<span data-ttu-id="eaf47-535">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-535">Yes</span></span>|<span data-ttu-id="eaf47-536">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-536">String</span></span>|<span data-ttu-id="eaf47-537">Hello tooapply tooeach elemento di condizione della matrice di origine hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="eaf47-538">Seleziona azione</span><span class="sxs-lookup"><span data-stu-id="eaf47-538">Select action</span></span>

<span data-ttu-id="eaf47-539">Hello `select` azione consente di ogni elemento della matrice di progetto in un nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="eaf47-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="eaf47-540">Ad esempio, tooconvert una matrice di numeri in una matrice di oggetti, è possibile utilizzare:</span><span class="sxs-lookup"><span data-stu-id="eaf47-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="eaf47-541">output di hello Hello `select` azione è una matrice con hello cardinalità stesso come hello matrice di input, con ogni elemento trasformato come definita da hello `select` proprietà.</span><span class="sxs-lookup"><span data-stu-id="eaf47-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="eaf47-542">Se l'input di hello è una matrice vuota, hello anche l'output è una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="eaf47-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="eaf47-543">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-543">Name</span></span>|<span data-ttu-id="eaf47-544">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-544">Required</span></span>|<span data-ttu-id="eaf47-545">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-545">Type</span></span>|<span data-ttu-id="eaf47-546">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="eaf47-547">from</span><span class="sxs-lookup"><span data-stu-id="eaf47-547">from</span></span>|<span data-ttu-id="eaf47-548">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-548">Yes</span></span>|<span data-ttu-id="eaf47-549">Array</span><span class="sxs-lookup"><span data-stu-id="eaf47-549">Array</span></span>|<span data-ttu-id="eaf47-550">Matrice di origine Hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-550">hello source array.</span></span>|
|<span data-ttu-id="eaf47-551">seleziona</span><span class="sxs-lookup"><span data-stu-id="eaf47-551">select</span></span>|<span data-ttu-id="eaf47-552">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-552">Yes</span></span>|<span data-ttu-id="eaf47-553">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="eaf47-553">Any</span></span>|<span data-ttu-id="eaf47-554">Hello proiezione tooapply tooeach elemento di matrice di origine hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="eaf47-555">Azione terminate</span><span class="sxs-lookup"><span data-stu-id="eaf47-555">Terminate action</span></span>

<span data-ttu-id="eaf47-556">azione di terminazione Hello interrompe l'esecuzione del hello del flusso di lavoro eseguito, l'interruzione di tutte le azioni in transito e ignorare tutte le azioni rimanenti.</span><span class="sxs-lookup"><span data-stu-id="eaf47-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="eaf47-557">Ad esempio, un'esecuzione con lo stato di tooterminate **non riuscito**, è possibile utilizzare hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="eaf47-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="eaf47-558">Già completate le azioni non sono interessate da hello terminare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="eaf47-559">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-559">Name</span></span>|<span data-ttu-id="eaf47-560">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-560">Required</span></span>|<span data-ttu-id="eaf47-561">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-561">Type</span></span>|<span data-ttu-id="eaf47-562">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="eaf47-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="eaf47-563">runStatus</span></span>|<span data-ttu-id="eaf47-564">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-564">Yes</span></span>|<span data-ttu-id="eaf47-565">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-565">String</span></span>|<span data-ttu-id="eaf47-566">destinazione Hello stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-566">hello target run status.</span></span> <span data-ttu-id="eaf47-567">**Failed** o **Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="eaf47-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="eaf47-568">runError</span><span class="sxs-lookup"><span data-stu-id="eaf47-568">runError</span></span>|<span data-ttu-id="eaf47-569">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-569">No</span></span>|<span data-ttu-id="eaf47-570">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-570">Object</span></span>|<span data-ttu-id="eaf47-571">dettagli dell'errore Hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-571">hello error details.</span></span> <span data-ttu-id="eaf47-572">Supportato quando solo **runStatus** è troppo**Failed**.</span><span class="sxs-lookup"><span data-stu-id="eaf47-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="eaf47-573">runError code</span><span class="sxs-lookup"><span data-stu-id="eaf47-573">runError code</span></span>|<span data-ttu-id="eaf47-574">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-574">No</span></span>|<span data-ttu-id="eaf47-575">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-575">String</span></span>|<span data-ttu-id="eaf47-576">Hello eseguire codice di errore.</span><span class="sxs-lookup"><span data-stu-id="eaf47-576">hello run error code.</span></span>|
|<span data-ttu-id="eaf47-577">runError message</span><span class="sxs-lookup"><span data-stu-id="eaf47-577">runError message</span></span>|<span data-ttu-id="eaf47-578">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-578">No</span></span>|<span data-ttu-id="eaf47-579">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-579">String</span></span>|<span data-ttu-id="eaf47-580">Hello eseguire messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="eaf47-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="eaf47-581">Azione compose</span><span class="sxs-lookup"><span data-stu-id="eaf47-581">Compose action</span></span>

<span data-ttu-id="eaf47-582">Hello Scrivi azione consente di costruire un oggetto arbitrario.</span><span class="sxs-lookup"><span data-stu-id="eaf47-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="eaf47-583">output di Hello di hello comporre azione hello risultato della valutazione relativi input.</span><span class="sxs-lookup"><span data-stu-id="eaf47-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="eaf47-584">Ad esempio, è possibile utilizzare hello comporre output toomerge azione di più azioni:</span><span class="sxs-lookup"><span data-stu-id="eaf47-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="eaf47-585">Hello **comporre** azione può essere utilizzato tooconstruct alcun output, inclusi gli oggetti, matrici e qualsiasi altro tipo supportato da app logica come XML e binario.</span><span class="sxs-lookup"><span data-stu-id="eaf47-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="eaf47-586">azione Tabella</span><span class="sxs-lookup"><span data-stu-id="eaf47-586">Table action</span></span>

<span data-ttu-id="eaf47-587">Hello `table` consente tooconvert una matrice di elementi in un **CSV** o **HTML** tabella.</span><span class="sxs-lookup"><span data-stu-id="eaf47-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="eaf47-588">Presumere che @triggerBody() sia</span><span class="sxs-lookup"><span data-stu-id="eaf47-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="eaf47-589">E consente di definire come azione hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="eaf47-590">produrrebbe Hello precedente</span><span class="sxs-lookup"><span data-stu-id="eaf47-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="eaf47-591">id</span><span class="sxs-lookup"><span data-stu-id="eaf47-591">id</span></span></th><th><span data-ttu-id="eaf47-592">name</span><span class="sxs-lookup"><span data-stu-id="eaf47-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="eaf47-593">0</span><span class="sxs-lookup"><span data-stu-id="eaf47-593">0</span></span></td><td><span data-ttu-id="eaf47-594">mele</span><span class="sxs-lookup"><span data-stu-id="eaf47-594">apples</span></span></td></tr><tr><td><span data-ttu-id="eaf47-595">1</span><span class="sxs-lookup"><span data-stu-id="eaf47-595">1</span></span></td><td><span data-ttu-id="eaf47-596">arance</span><span class="sxs-lookup"><span data-stu-id="eaf47-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="eaf47-597">"</span><span class="sxs-lookup"><span data-stu-id="eaf47-597">"</span></span>

<span data-ttu-id="eaf47-598">Nella tabella di hello toocustomize ordine, è possibile specificare colonne hello in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="eaf47-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="eaf47-599">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="eaf47-599">For example:</span></span>

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

<span data-ttu-id="eaf47-600">produrrebbe Hello precedente</span><span class="sxs-lookup"><span data-stu-id="eaf47-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="eaf47-601">ottenere ID</span><span class="sxs-lookup"><span data-stu-id="eaf47-601">produce id</span></span></th><th><span data-ttu-id="eaf47-602">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="eaf47-603">0</span><span class="sxs-lookup"><span data-stu-id="eaf47-603">0</span></span></td><td><span data-ttu-id="eaf47-604">mele fresche</span><span class="sxs-lookup"><span data-stu-id="eaf47-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="eaf47-605">1</span><span class="sxs-lookup"><span data-stu-id="eaf47-605">1</span></span></td><td><span data-ttu-id="eaf47-606">arance fresche</span><span class="sxs-lookup"><span data-stu-id="eaf47-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="eaf47-607">"</span><span class="sxs-lookup"><span data-stu-id="eaf47-607">"</span></span>

<span data-ttu-id="eaf47-608">Se hello `from` valore della proprietà è una matrice vuota, l'output di hello è una tabella vuota.</span><span class="sxs-lookup"><span data-stu-id="eaf47-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="eaf47-609">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-609">Name</span></span>|<span data-ttu-id="eaf47-610">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-610">Required</span></span>|<span data-ttu-id="eaf47-611">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-611">Type</span></span>|<span data-ttu-id="eaf47-612">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="eaf47-613">from</span><span class="sxs-lookup"><span data-stu-id="eaf47-613">from</span></span>|<span data-ttu-id="eaf47-614">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-614">Yes</span></span>|<span data-ttu-id="eaf47-615">Array</span><span class="sxs-lookup"><span data-stu-id="eaf47-615">Array</span></span>|<span data-ttu-id="eaf47-616">Matrice di origine Hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-616">hello source array.</span></span>|
|<span data-ttu-id="eaf47-617">format</span><span class="sxs-lookup"><span data-stu-id="eaf47-617">format</span></span>|<span data-ttu-id="eaf47-618">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-618">Yes</span></span>|<span data-ttu-id="eaf47-619">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-619">String</span></span>|<span data-ttu-id="eaf47-620">Hello formato, ovvero **CSV** o **HTML**.</span><span class="sxs-lookup"><span data-stu-id="eaf47-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="eaf47-621">columns</span><span class="sxs-lookup"><span data-stu-id="eaf47-621">columns</span></span>|<span data-ttu-id="eaf47-622">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-622">No</span></span>|<span data-ttu-id="eaf47-623">Array</span><span class="sxs-lookup"><span data-stu-id="eaf47-623">Array</span></span>|<span data-ttu-id="eaf47-624">colonne di Hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-624">hello columns.</span></span> <span data-ttu-id="eaf47-625">Consente a forma di toooverride hello predefinita della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="eaf47-626">intestazione di colonna</span><span class="sxs-lookup"><span data-stu-id="eaf47-626">column header</span></span>|<span data-ttu-id="eaf47-627">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-627">No</span></span>|<span data-ttu-id="eaf47-628">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-628">String</span></span>|<span data-ttu-id="eaf47-629">intestazione Hello della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-629">hello header of hello column.</span></span>|
|<span data-ttu-id="eaf47-630">valore colonna</span><span class="sxs-lookup"><span data-stu-id="eaf47-630">column value</span></span>|<span data-ttu-id="eaf47-631">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-631">Yes</span></span>|<span data-ttu-id="eaf47-632">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-632">String</span></span>|<span data-ttu-id="eaf47-633">valore di Hello della colonna hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="eaf47-634">Azione workflow</span><span class="sxs-lookup"><span data-stu-id="eaf47-634">Workflow action</span></span>   

|<span data-ttu-id="eaf47-635">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-635">Name</span></span>|<span data-ttu-id="eaf47-636">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-636">Required</span></span>|<span data-ttu-id="eaf47-637">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-637">Type</span></span>|<span data-ttu-id="eaf47-638">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-639">host id</span><span class="sxs-lookup"><span data-stu-id="eaf47-639">host id</span></span>|<span data-ttu-id="eaf47-640">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-640">Yes</span></span>|<span data-ttu-id="eaf47-641">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-641">String</span></span>|<span data-ttu-id="eaf47-642">ID di risorsa Hello del flusso di lavoro hello che si desidera toocall.</span><span class="sxs-lookup"><span data-stu-id="eaf47-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="eaf47-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="eaf47-643">host triggerName</span></span>|<span data-ttu-id="eaf47-644">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-644">Yes</span></span>|<span data-ttu-id="eaf47-645">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-645">String</span></span>|<span data-ttu-id="eaf47-646">nome di Hello del trigger hello che si desidera tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="eaf47-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="eaf47-647">query</span><span class="sxs-lookup"><span data-stu-id="eaf47-647">queries</span></span>|<span data-ttu-id="eaf47-648">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-648">No</span></span>|<span data-ttu-id="eaf47-649">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-649">Object</span></span>|<span data-ttu-id="eaf47-650">Rappresenta l'URL toohello tooadd i parametri della query hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="eaf47-651">Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="eaf47-652">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-652">headers</span></span>|<span data-ttu-id="eaf47-653">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-653">No</span></span>|<span data-ttu-id="eaf47-654">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-654">Object</span></span>|<span data-ttu-id="eaf47-655">Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di.</span><span class="sxs-lookup"><span data-stu-id="eaf47-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="eaf47-656">Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="eaf47-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="eaf47-657">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-657">body</span></span>|<span data-ttu-id="eaf47-658">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-658">No</span></span>|<span data-ttu-id="eaf47-659">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-659">Object</span></span>|<span data-ttu-id="eaf47-660">Rappresenta il payload di hello inviato toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="eaf47-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="eaf47-661">Viene eseguita una verifica di accesso nel flusso di lavoro hello \(in particolare, i trigger di hello\), ciò significa che è necessario accedere toohello del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="eaf47-662">Hello di output di hello `workflow` azione si basano su quelle definite nella hello `response` azione nel flusso di lavoro figlio hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="eaf47-663">Se non è stato definito uno `response` azione, quindi l'output di hello sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="eaf47-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="eaf47-664">Azione delle funzioni</span><span class="sxs-lookup"><span data-stu-id="eaf47-664">Function action</span></span>   

|<span data-ttu-id="eaf47-665">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-665">Name</span></span>|<span data-ttu-id="eaf47-666">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-666">Required</span></span>|<span data-ttu-id="eaf47-667">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-667">Type</span></span>|<span data-ttu-id="eaf47-668">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-669">function id</span><span class="sxs-lookup"><span data-stu-id="eaf47-669">function id</span></span>|<span data-ttu-id="eaf47-670">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-670">Yes</span></span>|<span data-ttu-id="eaf47-671">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-671">String</span></span>|<span data-ttu-id="eaf47-672">ID della funzione hello che si desidera tooinvoke risorsa Hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="eaf47-673">statico</span><span class="sxs-lookup"><span data-stu-id="eaf47-673">method</span></span>|<span data-ttu-id="eaf47-674">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-674">No</span></span>|<span data-ttu-id="eaf47-675">String</span><span class="sxs-lookup"><span data-stu-id="eaf47-675">String</span></span>|<span data-ttu-id="eaf47-676">Hello metodo HTTP utilizzato funzione hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="eaf47-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="eaf47-677">Per impostazione predefinita, è `POST` quando non è specificato.</span><span class="sxs-lookup"><span data-stu-id="eaf47-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="eaf47-678">query</span><span class="sxs-lookup"><span data-stu-id="eaf47-678">queries</span></span>|<span data-ttu-id="eaf47-679">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-679">No</span></span>|<span data-ttu-id="eaf47-680">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-680">Object</span></span>|<span data-ttu-id="eaf47-681">Rappresenta l'URL toohello tooadd i parametri della query hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="eaf47-682">Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="eaf47-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="eaf47-683">headers</span><span class="sxs-lookup"><span data-stu-id="eaf47-683">headers</span></span>|<span data-ttu-id="eaf47-684">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-684">No</span></span>|<span data-ttu-id="eaf47-685">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-685">Object</span></span>|<span data-ttu-id="eaf47-686">Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di.</span><span class="sxs-lookup"><span data-stu-id="eaf47-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="eaf47-687">Ad esempio, tooset hello lingua e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="eaf47-688">body</span><span class="sxs-lookup"><span data-stu-id="eaf47-688">body</span></span>|<span data-ttu-id="eaf47-689">No</span><span class="sxs-lookup"><span data-stu-id="eaf47-689">No</span></span>|<span data-ttu-id="eaf47-690">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-690">Object</span></span>|<span data-ttu-id="eaf47-691">Rappresenta il payload di hello inviato toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="eaf47-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="eaf47-692">Quando si salva hello logica app, si esegue alcuni controlli nella funzione hello a cui fa riferimento:</span><span class="sxs-lookup"><span data-stu-id="eaf47-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="eaf47-693">È necessario toohave access toohello (funzione).</span><span class="sxs-lookup"><span data-stu-id="eaf47-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="eaf47-694">È consentito solo il trigger HTTP standard o il trigger webhook JSON generico.</span><span class="sxs-lookup"><span data-stu-id="eaf47-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="eaf47-695">Non deve essere presente alcuna route definita.</span><span class="sxs-lookup"><span data-stu-id="eaf47-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="eaf47-696">Sono consentiti solo i livelli di autorizzazione "funzione" e "anonimo".</span><span class="sxs-lookup"><span data-stu-id="eaf47-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="eaf47-697">URL trigger Hello viene recuperato, memorizzato nella cache e utilizzato in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="eaf47-698">Pertanto, se qualsiasi operazione invalida URL memorizzati nella cache di hello, hello azione ha esito negativo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="eaf47-699">toowork il problema, salvare la logica app hello nuovamente, che causerà la logica app tooretrieve e memorizzare nella cache di hello trigger URL nuovamente.</span><span class="sxs-lookup"><span data-stu-id="eaf47-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="eaf47-700">Azioni di raccolta (ambiti e cicli)</span><span class="sxs-lookup"><span data-stu-id="eaf47-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="eaf47-701">Alcuni tipi di azioni possono contenere azioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="eaf47-702">Azioni di riferimento all'interno di una raccolta è possibile fare riferimento direttamente all'esterno di raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="eaf47-703">Se si è definito `http` in un ambito, `@body('http')` è ancora valido in qualsiasi punto del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="eaf47-704">Le azioni all'interno di una raccolta possono `runAfter` solo altre azioni all'interno di hello stessa raccolta.</span><span class="sxs-lookup"><span data-stu-id="eaf47-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="eaf47-705">Azione scope</span><span class="sxs-lookup"><span data-stu-id="eaf47-705">Scope action</span></span>

<span data-ttu-id="eaf47-706">Hello `scope` azione consente di raggruppare azioni in un flusso di lavoro in modo logico.</span><span class="sxs-lookup"><span data-stu-id="eaf47-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="eaf47-707">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-707">Name</span></span>|<span data-ttu-id="eaf47-708">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-708">Required</span></span>|<span data-ttu-id="eaf47-709">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-709">Type</span></span>|<span data-ttu-id="eaf47-710">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-711">Azioni</span><span class="sxs-lookup"><span data-stu-id="eaf47-711">actions</span></span>|<span data-ttu-id="eaf47-712">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-712">Yes</span></span>|<span data-ttu-id="eaf47-713">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-713">Object</span></span>|<span data-ttu-id="eaf47-714">Azioni interna tooexecute ambito hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="eaf47-715">Azione ForEach</span><span class="sxs-lookup"><span data-stu-id="eaf47-715">ForEach action</span></span>

<span data-ttu-id="eaf47-716">Questa azione di riproduzione a ciclo continuo scorre una matrice ed esegue azioni interne per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="eaf47-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="eaf47-717">Per impostazione predefinita, ciclo foreach hello esegue in parallelo (20 le esecuzioni in parallelo alla volta).</span><span class="sxs-lookup"><span data-stu-id="eaf47-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="eaf47-718">È possibile impostare regole di esecuzione utilizzando hello `operationOptions` parametro.</span><span class="sxs-lookup"><span data-stu-id="eaf47-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="eaf47-719">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-719">Name</span></span>|<span data-ttu-id="eaf47-720">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-720">Required</span></span>|<span data-ttu-id="eaf47-721">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-721">Type</span></span>|<span data-ttu-id="eaf47-722">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-723">Azioni</span><span class="sxs-lookup"><span data-stu-id="eaf47-723">actions</span></span>|<span data-ttu-id="eaf47-724">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-724">Yes</span></span>|<span data-ttu-id="eaf47-725">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-725">Object</span></span>|<span data-ttu-id="eaf47-726">Tooexecute interna azioni all'interno di ciclo hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="eaf47-727">foreach</span><span class="sxs-lookup"><span data-stu-id="eaf47-727">foreach</span></span>|<span data-ttu-id="eaf47-728">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-728">Yes</span></span>|<span data-ttu-id="eaf47-729">string</span><span class="sxs-lookup"><span data-stu-id="eaf47-729">string</span></span>|<span data-ttu-id="eaf47-730">Hello matrice tooiterate su</span><span class="sxs-lookup"><span data-stu-id="eaf47-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="eaf47-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="eaf47-731">operationOptions</span></span>|<span data-ttu-id="eaf47-732">no</span><span class="sxs-lookup"><span data-stu-id="eaf47-732">no</span></span>|<span data-ttu-id="eaf47-733">string</span><span class="sxs-lookup"><span data-stu-id="eaf47-733">string</span></span>|<span data-ttu-id="eaf47-734">Qualsiasi opzione di operazione per il comportamento.</span><span class="sxs-lookup"><span data-stu-id="eaf47-734">Any operation options for behavior.</span></span> <span data-ttu-id="eaf47-735">Attualmente supporta solo `sequential` tooexecute iterazioni in modo sequenziale (comportamento predefinito è parallelo)</span><span class="sxs-lookup"><span data-stu-id="eaf47-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="eaf47-736">Azione Until</span><span class="sxs-lookup"><span data-stu-id="eaf47-736">Until action</span></span>

<span data-ttu-id="eaf47-737">Questa azione ciclo esegue azioni interne fino a quando una condizione risultati tootrue.</span><span class="sxs-lookup"><span data-stu-id="eaf47-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="eaf47-738">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-738">Name</span></span>|<span data-ttu-id="eaf47-739">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-739">Required</span></span>|<span data-ttu-id="eaf47-740">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-740">Type</span></span>|<span data-ttu-id="eaf47-741">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-742">Azioni</span><span class="sxs-lookup"><span data-stu-id="eaf47-742">actions</span></span>|<span data-ttu-id="eaf47-743">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-743">Yes</span></span>|<span data-ttu-id="eaf47-744">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-744">Object</span></span>|<span data-ttu-id="eaf47-745">Tooexecute interna azioni all'interno di ciclo hello</span><span class="sxs-lookup"><span data-stu-id="eaf47-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="eaf47-746">expression</span><span class="sxs-lookup"><span data-stu-id="eaf47-746">expression</span></span>|<span data-ttu-id="eaf47-747">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-747">Yes</span></span>|<span data-ttu-id="eaf47-748">string</span><span class="sxs-lookup"><span data-stu-id="eaf47-748">string</span></span>|<span data-ttu-id="eaf47-749">Hello espressione tooevaluate dopo ogni iterazione</span><span class="sxs-lookup"><span data-stu-id="eaf47-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="eaf47-750">limit</span><span class="sxs-lookup"><span data-stu-id="eaf47-750">limit</span></span>|<span data-ttu-id="eaf47-751">sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-751">yes</span></span>|<span data-ttu-id="eaf47-752">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-752">Object</span></span>|<span data-ttu-id="eaf47-753">i limiti di Hello per ciclo hello - almeno un limite devono essere definiti</span><span class="sxs-lookup"><span data-stu-id="eaf47-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="eaf47-754">count</span><span class="sxs-lookup"><span data-stu-id="eaf47-754">count</span></span>|<span data-ttu-id="eaf47-755">no</span><span class="sxs-lookup"><span data-stu-id="eaf47-755">no</span></span>|<span data-ttu-id="eaf47-756">int</span><span class="sxs-lookup"><span data-stu-id="eaf47-756">int</span></span>|<span data-ttu-id="eaf47-757">Hello limitazione toohello del numero di iterazioni che possono essere eseguite</span><span class="sxs-lookup"><span data-stu-id="eaf47-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="eaf47-758">timeout</span><span class="sxs-lookup"><span data-stu-id="eaf47-758">timeout</span></span>|<span data-ttu-id="eaf47-759">no</span><span class="sxs-lookup"><span data-stu-id="eaf47-759">no</span></span>|<span data-ttu-id="eaf47-760">string</span><span class="sxs-lookup"><span data-stu-id="eaf47-760">string</span></span>|<span data-ttu-id="eaf47-761">timeout di Hello per quanto tempo deve ciclo.</span><span class="sxs-lookup"><span data-stu-id="eaf47-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="eaf47-762">Formato ISO 8601</span><span class="sxs-lookup"><span data-stu-id="eaf47-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="eaf47-763">Condizioni: azione If</span><span class="sxs-lookup"><span data-stu-id="eaf47-763">Conditions - If Action</span></span>

<span data-ttu-id="eaf47-764">Hello `If` azione consente di valutare una condizione ed eseguire un ramo in base che hello espressione troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="eaf47-765">Nome</span><span class="sxs-lookup"><span data-stu-id="eaf47-765">Name</span></span>|<span data-ttu-id="eaf47-766">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="eaf47-766">Required</span></span>|<span data-ttu-id="eaf47-767">Tipo</span><span class="sxs-lookup"><span data-stu-id="eaf47-767">Type</span></span>|<span data-ttu-id="eaf47-768">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eaf47-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="eaf47-769">Azioni</span><span class="sxs-lookup"><span data-stu-id="eaf47-769">actions</span></span>|<span data-ttu-id="eaf47-770">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-770">Yes</span></span>|<span data-ttu-id="eaf47-771">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-771">Object</span></span>|<span data-ttu-id="eaf47-772">Azioni interna tooexecute quando l'espressione restituisce troppo`true`</span><span class="sxs-lookup"><span data-stu-id="eaf47-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="eaf47-773">expression</span><span class="sxs-lookup"><span data-stu-id="eaf47-773">expression</span></span>|<span data-ttu-id="eaf47-774">Sì</span><span class="sxs-lookup"><span data-stu-id="eaf47-774">Yes</span></span>|<span data-ttu-id="eaf47-775">string</span><span class="sxs-lookup"><span data-stu-id="eaf47-775">string</span></span>|<span data-ttu-id="eaf47-776">Hello espressione tooevaluate</span><span class="sxs-lookup"><span data-stu-id="eaf47-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="eaf47-777">else</span><span class="sxs-lookup"><span data-stu-id="eaf47-777">else</span></span>|<span data-ttu-id="eaf47-778">no</span><span class="sxs-lookup"><span data-stu-id="eaf47-778">no</span></span>|<span data-ttu-id="eaf47-779">Oggetto</span><span class="sxs-lookup"><span data-stu-id="eaf47-779">Object</span></span>|<span data-ttu-id="eaf47-780">Azioni interna tooexecute quando l'espressione restituisce troppo`false`</span><span class="sxs-lookup"><span data-stu-id="eaf47-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="eaf47-781">Hello nella tabella seguente vengono illustrati esempi di condizioni di utilizzo espressioni in un'azione:</span><span class="sxs-lookup"><span data-stu-id="eaf47-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="eaf47-782">Valore JSON</span><span class="sxs-lookup"><span data-stu-id="eaf47-782">JSON value</span></span>|<span data-ttu-id="eaf47-783">Risultato</span><span class="sxs-lookup"><span data-stu-id="eaf47-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="eaf47-784">Qualsiasi valore valuterà tootrue provoca toopass questa condizione.</span><span class="sxs-lookup"><span data-stu-id="eaf47-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="eaf47-785">Sono supportate solo le espressioni booleane.</span><span class="sxs-lookup"><span data-stu-id="eaf47-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="eaf47-786">tooconvert altri tipi tooBoolean, utilizzare le funzioni `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="eaf47-787">Sono supportate le funzioni di confronto.</span><span class="sxs-lookup"><span data-stu-id="eaf47-787">Comparison functions are supported.</span></span> <span data-ttu-id="eaf47-788">Per questo esempio hello, l'azione di hello viene eseguita solo quando l'output di hello di act1 è maggiore del valore soglia hello.</span><span class="sxs-lookup"><span data-stu-id="eaf47-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="eaf47-789">Funzioni delle regole sono inoltre supportati toocreate nidificati espressioni booleane.</span><span class="sxs-lookup"><span data-stu-id="eaf47-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="eaf47-790">In questo caso, hello verrà eseguito quando l'output di hello del act1 è superiore alla soglia hello o inferiore a 100.</span><span class="sxs-lookup"><span data-stu-id="eaf47-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="eaf47-791">Se una matrice con tutti gli elementi, è possibile utilizzare toocheck funzioni di matrice.</span><span class="sxs-lookup"><span data-stu-id="eaf47-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="eaf47-792">In questo caso, hello verrà eseguito quando hello errori matrice è vuota.</span><span class="sxs-lookup"><span data-stu-id="eaf47-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="eaf47-793">Errore: condizione non valida perché @ è obbligatorio per le condizioni.</span><span class="sxs-lookup"><span data-stu-id="eaf47-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="eaf47-794">Se una condizione viene valutata correttamente, condizione hello è contrassegnato come `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="eaf47-795">Le azioni all'interno di uno hello `actions` o `else` oggetti valutare troppo`Succeeded` quando eseguita e ha avuto esito positivo, `Failed` quando eseguita e non è riuscita o `Skipped` quando non viene eseguita tale branch.</span><span class="sxs-lookup"><span data-stu-id="eaf47-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaf47-796">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eaf47-796">Next steps</span></span>

[<span data-ttu-id="eaf47-797">API REST del servizio flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="eaf47-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
