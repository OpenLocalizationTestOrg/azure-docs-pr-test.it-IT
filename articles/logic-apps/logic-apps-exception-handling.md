---
title: aaaError & eccezioni - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="669cc-103">Gestire errori ed eccezioni in App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="669cc-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="669cc-104">Le app di logica di Azure fornisce strumenti avanzati e toohelp modelli assicurarsi che le integrazioni sono affidabile e resiliente agli errori.</span><span class="sxs-lookup"><span data-stu-id="669cc-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="669cc-105">Qualsiasi architettura di integrazione pone hello problema del tempo di inattività che tooappropriately handle o problemi da sistemi dipendenti.</span><span class="sxs-lookup"><span data-stu-id="669cc-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="669cc-106">Gestione degli errori di logica App rende un'esperienza di prima classe, offrendo hello gli strumenti necessari tooact in eccezioni ed errori nei flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="669cc-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="669cc-107">Criteri di ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="669cc-107">Retry policies</span></span>

<span data-ttu-id="669cc-108">Un criterio di ripetizione è di tipo di eccezione e la gestione degli errori di base hello.</span><span class="sxs-lookup"><span data-stu-id="669cc-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="669cc-109">Se una richiesta iniziale è scaduto oppure non è riuscita (qualsiasi richiesta che comporta un 429 o risposta 5xx), questo criterio definisce se deve ritentare l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="669cc-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="669cc-110">Per impostazione predefinita, tutte le azioni vengono ripetute altre 4 volte a intervalli di 20 secondi.</span><span class="sxs-lookup"><span data-stu-id="669cc-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="669cc-111">Pertanto, se prima richiesta hello riceve un `500 Internal Server Error` risposta, il motore di flusso di lavoro hello sospende per 20 secondi, e tentativi hello richiesta nuovamente.</span><span class="sxs-lookup"><span data-stu-id="669cc-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="669cc-112">Se dopo tutti i tentativi, risposta hello è ancora un errore o eccezione, il flusso di hello continua e segni di hello stato dell'azione come `Failed`.</span><span class="sxs-lookup"><span data-stu-id="669cc-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="669cc-113">È possibile configurare criteri di tentativi in hello **input** per una determinata azione.</span><span class="sxs-lookup"><span data-stu-id="669cc-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="669cc-114">Ad esempio, è possibile configurare un tootry di criteri di tentativi fino a 4 volte per gli intervalli di 1 ora.</span><span class="sxs-lookup"><span data-stu-id="669cc-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="669cc-115">Per altre informazioni sulle proprietà di input, vedere [Azioni e trigger del flusso di lavoro][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="669cc-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="669cc-116">Se si desidera il tooretry di azione HTTP 4 volte, attendere 10 minuti tra ogni tentativo di utilizzare hello seguente definizione:</span><span class="sxs-lookup"><span data-stu-id="669cc-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

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

<span data-ttu-id="669cc-117">Per ulteriori informazioni sulla sintassi supportata, vedere hello [sezione criteri di ripetizione di azioni del flusso di lavoro e i trigger][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="669cc-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="669cc-118">Intercettare gli errori con hello RunAfter proprietà</span><span class="sxs-lookup"><span data-stu-id="669cc-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="669cc-119">Ogni azione di logica app dichiara le azioni che devono essere completata prima dell'inizio azione hello, ad esempio ordinamento passaggi hello nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="669cc-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="669cc-120">Nella definizione di azione hello, questo ordinamento è noto come hello `runAfter` proprietà.</span><span class="sxs-lookup"><span data-stu-id="669cc-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="669cc-121">Questa proprietà è un oggetto che descrive le azioni e gli stati di azione eseguire l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="669cc-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="669cc-122">Per impostazione predefinita, tutte le azioni aggiunte tramite Progettazione applicazione logica hello sono troppo`runAfter` hello precedenza se hello passaggio precedente `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="669cc-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="669cc-123">Tuttavia, è possibile personalizzare le azioni toofire questo valore quando le azioni precedenti hanno `Failed`, `Skipped`, o un set di possibili valori sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="669cc-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="669cc-124">Se si desiderava tooadd tooa un elemento designato come argomento del Bus di servizio dopo un'azione specifica `Insert_Row` ha esito negativo, è possibile utilizzare hello seguente `runAfter` configurazione:</span><span class="sxs-lookup"><span data-stu-id="669cc-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

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

<span data-ttu-id="669cc-125">Hello preavviso `runAfter` proprietà viene impostata toofire se hello `Insert_Row` azione `Failed`.</span><span class="sxs-lookup"><span data-stu-id="669cc-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="669cc-126">azione di hello toorun se è stato dell'azione hello `Succeeded`, `Failed`, o `Skipped`, utilizzare la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="669cc-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="669cc-127">Le azioni eseguite dopo l'esito negativo di un'azione precedente e completate correttamente vengono contrassegnate come `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="669cc-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="669cc-128">Ciò significa che se si catch tutti correttamente gli errori in un flusso di lavoro hello eseguito è contrassegnato come `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="669cc-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="669cc-129">Azioni tooevaluate ambiti e risultati</span><span class="sxs-lookup"><span data-stu-id="669cc-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="669cc-130">Toohow simile è possibile eseguire dopo le singole azioni, è possibile anche raggruppare azioni all'interno di un [ambito](../logic-apps/logic-apps-loops-and-scopes.md), che fungono da un raggruppamento logico di azioni.</span><span class="sxs-lookup"><span data-stu-id="669cc-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="669cc-131">Gli ambiti sono utili per organizzare le azioni di app logica e per l'esecuzione di valutazioni di aggregazione in stato di hello di un ambito.</span><span class="sxs-lookup"><span data-stu-id="669cc-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="669cc-132">ambito Hello stesso riceve lo stato dopo aver completato tutte le azioni in un ambito.</span><span class="sxs-lookup"><span data-stu-id="669cc-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="669cc-133">stato dell'ambito Hello è determinato con hello un'esecuzione agli stessi criteri.</span><span class="sxs-lookup"><span data-stu-id="669cc-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="669cc-134">Se hello azione finale in un branch di esecuzione è `Failed` o `Aborted`, lo stato di hello è `Failed`.</span><span class="sxs-lookup"><span data-stu-id="669cc-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="669cc-135">toofire azioni specifiche per eventuali errori che si sono verificati nell'ambito di hello, è possibile utilizzare `runAfter` con un ambito che è contrassegnato come `Failed`.</span><span class="sxs-lookup"><span data-stu-id="669cc-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="669cc-136">Se *qualsiasi* azioni nell'ambito di hello non riescono, in esecuzione dopo un ambito ha esito negativo consente di creare una singola azione toocatch errori.</span><span class="sxs-lookup"><span data-stu-id="669cc-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="669cc-137">Ottenere il contesto di hello degli errori relativi a risultati</span><span class="sxs-lookup"><span data-stu-id="669cc-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="669cc-138">Sebbene intercettare gli errori di un ambito è utile, è possibile anche toohelp di contesto che è comprendere esattamente le azioni che non è riuscite, ed eventuali errori o codici di stato che sono stati restituiti.</span><span class="sxs-lookup"><span data-stu-id="669cc-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="669cc-139">Hello `@result()` funzione del flusso di lavoro fornisce un contesto sul risultato di hello di tutte le azioni in un ambito.</span><span class="sxs-lookup"><span data-stu-id="669cc-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="669cc-140">`@result()`accetta un singolo parametro, il nome dell'ambito e restituisce una matrice di tutti i risultati dell'azione hello da tale ambito.</span><span class="sxs-lookup"><span data-stu-id="669cc-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="669cc-141">Questi oggetti azione includono hello stesso gli attributi come hello `@actions()` Genera oggetto, inclusi l'ora di inizio azione, ora di fine di azione, lo stato di azione, input azione, ID di correlazione di azione e azione.</span><span class="sxs-lookup"><span data-stu-id="669cc-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="669cc-142">contesto toosend di tutte le azioni che non è riuscita in un ambito, può facilmente associare un `@result()` funzione con un `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="669cc-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="669cc-143">tooexecute un'azione *per ogni* azione in un ambito che `Failed`tooactions risultati matrice hello filtro che non è riuscita, è possibile associare `@result()` con un  **[filtro matrice](../connectors/connectors-native-query.md)**  azione e un  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  ciclo.</span><span class="sxs-lookup"><span data-stu-id="669cc-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="669cc-144">È possibile richiedere la matrice dei risultati filtrati hello ed eseguire un'azione per ogni errore utilizzando hello **ForEach** ciclo.</span><span class="sxs-lookup"><span data-stu-id="669cc-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="669cc-145">Di seguito è riportato un esempio, seguito da una spiegazione dettagliata, che invia una richiesta HTTP POST con il corpo di risposta hello di tutte le azioni che non è nell'ambito di hello `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="669cc-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

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

<span data-ttu-id="669cc-146">Di seguito è riportato un toodescribe dettagliata cosa accade:</span><span class="sxs-lookup"><span data-stu-id="669cc-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="669cc-147">tutte le azioni all'interno di risultato hello tooget `My_Scope`, hello **filtro matrice** filtri azione `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="669cc-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="669cc-148">Hello condizione per **filtro matrice** qualsiasi `@result()` elemento il cui stato uguale troppo`Failed`.</span><span class="sxs-lookup"><span data-stu-id="669cc-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="669cc-149">Questa condizione filtri matrice hello con tutti i risultati dell'azione da `My_Scope` tooan matrice con solo non è stato possibile risultati dell'azione.</span><span class="sxs-lookup"><span data-stu-id="669cc-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="669cc-150">Eseguire un **per ogni** azione hello **matrice filtrata** output.</span><span class="sxs-lookup"><span data-stu-id="669cc-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="669cc-151">Questo passaggio esegue un'azione *per ogni* risultato di azione non riuscita precedentemente filtrato.</span><span class="sxs-lookup"><span data-stu-id="669cc-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="669cc-152">Se non è riuscita un'unica azione nell'ambito di hello, hello azioni in hello `foreach` eseguire una sola volta.</span><span class="sxs-lookup"><span data-stu-id="669cc-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="669cc-153">Molte azioni non riuscite determinano un'azione per errore.</span><span class="sxs-lookup"><span data-stu-id="669cc-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="669cc-154">Inviare una richiesta POST HTTP su hello `foreach` elemento corpo della risposta, o `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="669cc-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="669cc-155">Hello `@result()` è hello stessa forma di elemento come hello `@actions()` forma e può essere analizzato hello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="669cc-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="669cc-156">Includere due intestazioni personalizzate con il nome di azione non riuscita hello `@item()['name']` e hello non è stato possibile eseguire client ID rilevamento `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="669cc-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="669cc-157">Per riferimento, di seguito è riportato un esempio di un singolo `@result()` elemento, che mostra hello `name`, `body`, e `clientTrackingId` le proprietà che vengono analizzate nell'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="669cc-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="669cc-158">All'esterno di `foreach`, `@result()` restituisce una matrice di questi oggetti.</span><span class="sxs-lookup"><span data-stu-id="669cc-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="669cc-159">tooperform eccezioni diversi modelli, è possibile utilizzare espressioni di hello illustrate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="669cc-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="669cc-160">Si potrebbe scegliere tooexecute un'unica eccezione che gestisce l'azione di fuori ambito hello che accetta l'intera matrice filtrata di hello di errori e rimuovere hello `foreach`.</span><span class="sxs-lookup"><span data-stu-id="669cc-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="669cc-161">È inoltre possibile includere altre proprietà utili da hello `@result()` risposta illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="669cc-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="669cc-162">Diagnostica e telemetria di Azure</span><span class="sxs-lookup"><span data-stu-id="669cc-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="669cc-163">Hello precedenti sono consigliato toohandle errori ed eccezioni all'interno di un'esecuzione, ma è anche possibile identificare e rispondere tooerrors indipendente di hello eseguito.</span><span class="sxs-lookup"><span data-stu-id="669cc-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="669cc-164">[Diagnostica di Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fornisce un modo semplice di toosend tutti account di archiviazione Azure tooan di eventi (inclusi tutti gli stati di esecuzione e l'azione) del flusso di lavoro o un Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="669cc-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="669cc-165">tooevaluate gli stati di esecuzione, è possibile monitorare le metriche e i registri di hello o pubblicarli in qualsiasi strumento di monitoraggio che si preferisce.</span><span class="sxs-lookup"><span data-stu-id="669cc-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="669cc-166">Potenziale è toostream tutti gli eventi di hello tramite Hub di eventi di Azure in [Analitica flusso](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="669cc-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="669cc-167">Nel flusso Analitica, è possibile scrivere query in tempo reale disattivare eventuali anomalie, medie o errori da hello i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="669cc-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="669cc-168">Flusso Analitica può facilmente output tooother di origini dati quali code, argomenti, SQL, database Cosmos di Azure e Power BI.</span><span class="sxs-lookup"><span data-stu-id="669cc-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="669cc-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="669cc-169">Next Steps</span></span>

* [<span data-ttu-id="669cc-170">Informazioni su come un cliente ha implementato una solida gestione delle eccezioni con App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="669cc-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="669cc-171">Altri esempi e scenari di app per la logica</span><span class="sxs-lookup"><span data-stu-id="669cc-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="669cc-172">Informazioni su come toocreate automatizzare le distribuzioni per App per la logica</span><span class="sxs-lookup"><span data-stu-id="669cc-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="669cc-173">Compilare e distribuire app per la logica con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="669cc-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
