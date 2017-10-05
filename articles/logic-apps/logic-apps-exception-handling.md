---
title: Gestione delle eccezioni e degli errori - App per la logica di Azure | Documentazione Microsoft
description: Modelli per la gestione degli errori e delle eccezioni in App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="12167-103">Gestire errori ed eccezioni in App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="12167-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="12167-104">App per la logica di Azure offre un set completo di strumenti e modelli per garantire la solidità e la resilienza delle integrazioni dell'utente in caso di errori.</span><span class="sxs-lookup"><span data-stu-id="12167-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="12167-105">In qualsiasi architettura di integrazione, una delle sfide è garantire che i tempi di inattività o i problemi dei sistemi dipendenti vengano gestiti in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="12167-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="12167-106">App per la logica ottimizza la gestione degli errori offrendo gli strumenti necessari per intervenire in caso di eccezioni ed errori nei flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="12167-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="12167-107">Criteri di ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="12167-107">Retry policies</span></span>

<span data-ttu-id="12167-108">Il tipo più semplice di gestione degli errori e delle eccezioni è costituito dai criteri di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="12167-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="12167-109">Tali criteri definiscono se l'azione dovrà essere ripetuta in caso di timeout o esito negativo (con restituzione di una risposta 429 o 5xx) della richiesta iniziale.</span><span class="sxs-lookup"><span data-stu-id="12167-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="12167-110">Per impostazione predefinita, tutte le azioni vengono ripetute altre 4 volte a intervalli di 20 secondi.</span><span class="sxs-lookup"><span data-stu-id="12167-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="12167-111">Se la prima richiesta ha ricevuto una risposta `500 Internal Server Error`, il motore del flusso di lavoro viene sospeso per 20 secondi e quindi ripete la richiesta.</span><span class="sxs-lookup"><span data-stu-id="12167-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="12167-112">Se dopo tutti i tentativi la risposta è ancora un'eccezione o un errore, il flusso di lavoro continua e contrassegna l'azione con lo stato `Failed`.</span><span class="sxs-lookup"><span data-stu-id="12167-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="12167-113">È possibile configurare i criteri di ripetizione dei tentativi nelle proprietà **input** di una determinata azione.</span><span class="sxs-lookup"><span data-stu-id="12167-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="12167-114">Ad esempio, i criteri di ripetizione possono essere configurati fino a un massimo di 4 tentativi a intervalli di 1 ora.</span><span class="sxs-lookup"><span data-stu-id="12167-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="12167-115">Per altre informazioni sulle proprietà di input, vedere [Azioni e trigger del flusso di lavoro][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="12167-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="12167-116">Se si vuole che l'azione HTTP venga ripetuta 4 volte con un'attesa di 10 minuti tra i singoli tentativi, usare la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="12167-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="12167-117">Per altre informazioni sulla sintassi supportata, vedere la [sezione relativa ai criteri di ripetizione dei tentativi in Azioni e trigger del flusso di lavoro][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="12167-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="12167-118">Rilevare gli errori con la proprietà runAfter</span><span class="sxs-lookup"><span data-stu-id="12167-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="12167-119">Ogni azione di un'app per la logica dichiara le azioni che devono essere completate prima del proprio avvio. Si ottiene così una sorta di ordinamento dei passaggi del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="12167-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="12167-120">Tale ordinamento è costituito dalla proprietà `runAfter` nella definizione dell'azione,</span><span class="sxs-lookup"><span data-stu-id="12167-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="12167-121">un oggetto che descrive le azioni e gli stati delle azioni che determineranno l'esecuzione dell'azione.</span><span class="sxs-lookup"><span data-stu-id="12167-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="12167-122">Per impostazione predefinita, tutte le azioni aggiunte tramite la finestra di progettazione di app per la logica vengono impostate per essere eseguite dopo il passaggio precedente (`runAfter`) se il passaggio precedente risulta `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="12167-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="12167-123">È possibile personalizzare questo valore per attivare le azioni quando lo stato delle azioni precedenti è `Failed`, `Skipped` o un possibile insieme di questi valori.</span><span class="sxs-lookup"><span data-stu-id="12167-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="12167-124">Se si vuole aggiungere un elemento a un argomento del bus di servizio designato dopo l'esito negativo di una specifica azione `Insert_Row`, usare la configurazione `runAfter` seguente:</span><span class="sxs-lookup"><span data-stu-id="12167-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="12167-125">Si noti che la proprietà `runAfter` è impostata per essere attivata se l'azione `Insert_Row` è `Failed`.</span><span class="sxs-lookup"><span data-stu-id="12167-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="12167-126">Per eseguire l'azione se lo stato dell'azione è `Succeeded`, `Failed` o `Skipped`, usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="12167-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="12167-127">Le azioni eseguite dopo l'esito negativo di un'azione precedente e completate correttamente vengono contrassegnate come `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="12167-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="12167-128">Con questo comportamento, se tutti gli errori in un flusso di lavoro vengono rilevati l'esecuzione stessa verrà contrassegnata come `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="12167-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="12167-129">Ambiti e risultati per la valutazione delle azioni</span><span class="sxs-lookup"><span data-stu-id="12167-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="12167-130">Così come è possibile configurare l'esecuzione dopo singole azioni, è anche possibile raggruppare insieme le azioni all'interno di un [ambito](../logic-apps/logic-apps-loops-and-scopes.md), che fungerà da raggruppamento logico delle azioni.</span><span class="sxs-lookup"><span data-stu-id="12167-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="12167-131">Gli ambiti sono utili sia per organizzare le azioni delle app per la logica sia per eseguire valutazioni aggregate sullo stato di un ambito.</span><span class="sxs-lookup"><span data-stu-id="12167-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="12167-132">L'ambito in sé riceve uno stato dopo che sono state completate tutte le azioni al suo interno.</span><span class="sxs-lookup"><span data-stu-id="12167-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="12167-133">Lo stato dell'ambito è determinato con gli stessi criteri usati per un'esecuzione:</span><span class="sxs-lookup"><span data-stu-id="12167-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="12167-134">se l'azione finale in un ramo di esecuzione è `Failed` o `Aborted`, lo stato è `Failed`.</span><span class="sxs-lookup"><span data-stu-id="12167-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="12167-135">È possibile usare `runAfter` dopo che è un ambito è stato contrassegnato come `Failed` per attivare azioni specifiche per gli eventuali errori verificatisi all'interno dell'ambito.</span><span class="sxs-lookup"><span data-stu-id="12167-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="12167-136">L'esecuzione dopo l'esito negativo di un ambito consente di creare una singola azione per rilevare gli errori in caso di esito negativo di *qualsiasi* azione all'interno dell'ambito.</span><span class="sxs-lookup"><span data-stu-id="12167-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="12167-137">Recupero del contesto degli errori con i risultati</span><span class="sxs-lookup"><span data-stu-id="12167-137">Getting the context of failures with results</span></span>

<span data-ttu-id="12167-138">Rilevare gli errori è molto utile, ma può essere opportuno anche il contesto per comprendere esattamente quali azioni hanno avuto esito negativo e tutti gli errori o i codici di stato restituiti.</span><span class="sxs-lookup"><span data-stu-id="12167-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="12167-139">La funzione `@result()` del flusso di lavoro offre il contesto relativo al risultato di tutte le azioni all'interno di un ambito.</span><span class="sxs-lookup"><span data-stu-id="12167-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="12167-140">`@result()` accetta un unico parametro, il nome dell'ambito, e restituisce una matrice dei risultati di tutte le azioni di tale ambito.</span><span class="sxs-lookup"><span data-stu-id="12167-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="12167-141">Tali oggetti azione includono gli stessi attributi dell'oggetto `@actions()` , come ora di inizio, ora di fine, stato, input, ID di correlazione e output dell'azione.</span><span class="sxs-lookup"><span data-stu-id="12167-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="12167-142">Per inviare il contesto di qualsiasi azione non riuscita all'interno di un ambito, è possibile associare una funzione `@result()` a `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="12167-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="12167-143">Se si vuole eseguire un'azione *per ogni* azione di un ambito con stato `Failed`, è possibile associare `@result()` a un'azione **[Filtra matrice](../connectors/connectors-native-query.md)** e a un ciclo **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**. Ciò consente di filtrare la matrice dei risultati in modo da ottenere le azioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="12167-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="12167-144">La matrice dei risultati filtrata può quindi essere usata per eseguire un'azione per ogni errore con il ciclo **ForEach** .</span><span class="sxs-lookup"><span data-stu-id="12167-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="12167-145">L'esempio seguente, seguito da una spiegazione dettagliata, invia una richiesta HTTP POST con il corpo della risposta di qualsiasi azione non riuscita all'interno dell'ambito `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="12167-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="12167-146">Ecco la procedura dettagliata eseguita:</span><span class="sxs-lookup"><span data-stu-id="12167-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="12167-147">Per ottenere il risultato di tutte le azioni all'interno di `My_Scope`, l'azione **Filtra matrice** filtra `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="12167-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="12167-148">La condizione per **Filtra matrice** è qualsiasi elemento `@result()` con stato uguale a `Failed`.</span><span class="sxs-lookup"><span data-stu-id="12167-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="12167-149">Questa condizione filtra la matrice con tutti i risultati dell'azione da `My_Scope` a una matrice con i soli risultati delle azioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="12167-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="12167-150">Esecuzione di un'azione **For Each** sugli output **Matrice filtrata**.</span><span class="sxs-lookup"><span data-stu-id="12167-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="12167-151">Questo passaggio esegue un'azione *per ogni* risultato di azione non riuscita precedentemente filtrato.</span><span class="sxs-lookup"><span data-stu-id="12167-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="12167-152">Se una sola azione nell'ambito ha avuto esito negativo, le azioni in `foreach` vengono eseguite una sola volta.</span><span class="sxs-lookup"><span data-stu-id="12167-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="12167-153">Molte azioni non riuscite determinano un'azione per errore.</span><span class="sxs-lookup"><span data-stu-id="12167-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="12167-154">Invio di HTTP POST nel corpo della risposta dell'elemento `foreach`, ovvero `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="12167-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="12167-155">La forma dell'elemento `@result()` è uguale alla forma di `@actions()` e può essere analizzata nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="12167-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="12167-156">Inclusione di due intestazioni personalizzate con il nome dell'azione non riuscita `@item()['name']` e l'ID rilevamento client dell'esecuzione non riuscita `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="12167-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="12167-157">Come riferimento, di seguito è riportato un esempio di un singolo elemento `@result()`, che mostra le proprietà `name`, `body`, e `clientTrackingId` analizzate nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="12167-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="12167-158">All'esterno di `foreach`, `@result()` restituisce una matrice di questi oggetti.</span><span class="sxs-lookup"><span data-stu-id="12167-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="12167-159">Le espressioni riportate sopra possono essere usate per eseguire diversi modelli di gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="12167-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="12167-160">È possibile scegliere di eseguire una singola azione di gestione delle eccezioni all'esterno dell'ambito che accetta l'intera matrice filtrata degli errori e rimuovere `foreach`.</span><span class="sxs-lookup"><span data-stu-id="12167-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="12167-161">È anche possibile includere altre proprietà utili della risposta `@result()` illustrata sopra.</span><span class="sxs-lookup"><span data-stu-id="12167-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="12167-162">Diagnostica e telemetria di Azure</span><span class="sxs-lookup"><span data-stu-id="12167-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="12167-163">I modelli precedenti sono un ottimo modo per gestire gli errori e le eccezioni in un'esecuzione, ma è possibile anche identificare e rispondere agli errori indipendentemente dall'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="12167-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="12167-164">[Diagnostica di Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) consente di inviare in modo semplice tutti gli eventi del flusso di lavoro (inclusi tutti gli stati delle esecuzioni e delle azioni) a un account di archiviazione di Azure o un hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="12167-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="12167-165">Per valutare gli stati delle esecuzioni è possibile monitorare i log e le metriche o pubblicarli nello strumento di monitoraggio preferito.</span><span class="sxs-lookup"><span data-stu-id="12167-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="12167-166">Una possibile opzione consiste nel trasmettere tutti gli eventi tramite un hub eventi di Azure ad [Analisi di flusso](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="12167-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="12167-167">In Analisi di flusso è possibile scrivere query dinamiche per qualsiasi anomalia, media o errore dei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="12167-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="12167-168">Analisi di flusso può facilmente inviare output ad altre origini dati come query, argomenti, SQL, Cosmos DB e Power BI.</span><span class="sxs-lookup"><span data-stu-id="12167-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12167-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12167-169">Next Steps</span></span>

* [<span data-ttu-id="12167-170">Informazioni su come un cliente ha implementato una solida gestione delle eccezioni con App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="12167-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="12167-171">Altri esempi e scenari di app per la logica</span><span class="sxs-lookup"><span data-stu-id="12167-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="12167-172">Informazioni su come creare distribuzioni automatizzate di app per la logica</span><span class="sxs-lookup"><span data-stu-id="12167-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="12167-173">Compilare e distribuire app per la logica con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12167-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
