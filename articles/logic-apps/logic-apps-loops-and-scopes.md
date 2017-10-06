---
title: cicli e gli ambiti o debatch dati nei flussi di lavoro - App Azure per la logica aaaCreate | Documenti Microsoft
description: "Creare cicli tooiterate tra i dati, le azioni in ambiti, gruppo o debatch toostart dati più flussi di lavoro in Azure App per la logica."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="12b60-103">Cicli, ambiti e debatching delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="12b60-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="12b60-104">Logica App offre una serie di modi toowork con matrici, raccolte, batch e cicli all'interno di un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="12b60-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="12b60-105">Matrici e cicli ForEach</span><span class="sxs-lookup"><span data-stu-id="12b60-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="12b60-106">Logica App consente tooloop su un set di dati ed eseguire un'azione per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="12b60-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="12b60-107">Ciò è possibile tramite hello `foreach` azione.</span><span class="sxs-lookup"><span data-stu-id="12b60-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="12b60-108">Nella finestra di progettazione hello, è possibile specificare tooadd una per ogni ciclo.</span><span class="sxs-lookup"><span data-stu-id="12b60-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="12b60-109">Dopo aver selezionato una matrice di hello desiderato tooiterate tramite, è possibile iniziare l'aggiunta di azioni.</span><span class="sxs-lookup"><span data-stu-id="12b60-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="12b60-110">Sono attualmente limitate tooonly un'azione per ogni ciclo foreach, ma questa limitazione verrà rimossa in hello in arrivo settimane.</span><span class="sxs-lookup"><span data-stu-id="12b60-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="12b60-111">Una volta all'interno di ciclo hello è possibile iniziare toospecify cosa dovrebbe accadere in ogni valore di matrice hello.</span><span class="sxs-lookup"><span data-stu-id="12b60-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="12b60-112">Se si usa la visualizzazione del codice, è possibile specificare un loop ForEach come nell'illustrazione che segue.</span><span class="sxs-lookup"><span data-stu-id="12b60-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="12b60-113">In questo esempio di loop ForEach viene inviato un messaggio di posta elettronica per ogni indirizzo di posta elettronica che contiene "microsoft.com":</span><span class="sxs-lookup"><span data-stu-id="12b60-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
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
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="12b60-114">Oggetto `foreach` azione possibile scorrere le matrici di too5, 000 righe.</span><span class="sxs-lookup"><span data-stu-id="12b60-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="12b60-115">Per impostazione predefinita, ogni iterazione verrà eseguita in parallelo alle altre.</span><span class="sxs-lookup"><span data-stu-id="12b60-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="12b60-116">Cicli ForEach sequenziali</span><span class="sxs-lookup"><span data-stu-id="12b60-116">Sequential ForEach loops</span></span>

<span data-ttu-id="12b60-117">tooenable un tooexecute ciclo foreach in sequenza, hello `Sequential` deve essere aggiunta l'opzione di operazione.</span><span class="sxs-lookup"><span data-stu-id="12b60-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="12b60-118">Ciclo Until</span><span class="sxs-lookup"><span data-stu-id="12b60-118">Until loop</span></span>
  
  <span data-ttu-id="12b60-119">È possibile eseguire un'azione o una serie di azioni finché non viene soddisfatta una condizione.</span><span class="sxs-lookup"><span data-stu-id="12b60-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="12b60-120">Hello scenario più comune per questo consiste nel chiamare un endpoint fino a ottenere una risposta hello che si sta cercando.</span><span class="sxs-lookup"><span data-stu-id="12b60-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="12b60-121">Nella finestra di progettazione hello, è possibile specificare tooadd un fino al ciclo.</span><span class="sxs-lookup"><span data-stu-id="12b60-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="12b60-122">Dopo l'aggiunta di azioni all'interno di ciclo hello, è possibile impostare la condizione di uscita hello, nonché hello i limiti di ciclo.</span><span class="sxs-lookup"><span data-stu-id="12b60-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="12b60-123">Si verifica un ritardo di 1 minuto tra i cicli del loop.</span><span class="sxs-lookup"><span data-stu-id="12b60-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="12b60-124">Se si usa la visualizzazione del codice, è possibile specificare un loop Until come nell'illustrazione che segue.</span><span class="sxs-lookup"><span data-stu-id="12b60-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="12b60-125">Questo è un esempio di chiamata di un endpoint HTTP finché il corpo della risposta hello è il valore di hello 'Completato'.</span><span class="sxs-lookup"><span data-stu-id="12b60-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="12b60-126">Ciò avviene in presenza di una di queste condizioni:</span><span class="sxs-lookup"><span data-stu-id="12b60-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="12b60-127">Lo stato della risposta HTTP è "Completed"</span><span class="sxs-lookup"><span data-stu-id="12b60-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="12b60-128">Sono stati fatti tentativi per 1 ora</span><span class="sxs-lookup"><span data-stu-id="12b60-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="12b60-129">Il ciclo è stato eseguito 100 volte</span><span class="sxs-lookup"><span data-stu-id="12b60-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="12b60-130">SplitOn e scomposizione batch</span><span class="sxs-lookup"><span data-stu-id="12b60-130">SplitOn and debatching</span></span>

<span data-ttu-id="12b60-131">In alcuni casi un trigger può ricevere una matrice di elementi desiderati toodebatch e avviare un flusso di lavoro per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="12b60-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="12b60-132">Questo può essere eseguito tramite hello `spliton` comando.</span><span class="sxs-lookup"><span data-stu-id="12b60-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="12b60-133">Per impostazione predefinita, se lo swagger del trigger specifica un payload che è una matrice, viene aggiunto `spliton` e viene avviata un'esecuzione per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="12b60-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="12b60-134">SplitOn possono essere aggiunti solo tooa trigger.</span><span class="sxs-lookup"><span data-stu-id="12b60-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="12b60-135">L'operazione può essere configurata manualmente o sottoposta a override nella visualizzazione del codice di definizione.</span><span class="sxs-lookup"><span data-stu-id="12b60-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="12b60-136">Attualmente è possibile SplitOn debatch matrici backup too5, gli elementi 000.</span><span class="sxs-lookup"><span data-stu-id="12b60-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="12b60-137">Non è possibile avere un `spliton` e inoltre implementare il modello di risposta sincrona hello.</span><span class="sxs-lookup"><span data-stu-id="12b60-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="12b60-138">Qualsiasi flusso di lavoro denominato che ha un `response` azione inoltre troppo`spliton` verrà eseguito in modo asincrono e inviare immediatamente `202 Accepted` risposta.</span><span class="sxs-lookup"><span data-stu-id="12b60-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="12b60-139">SplitOn può essere specificato nella visualizzazione codice come hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="12b60-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="12b60-140">In questo caso viene ricevuta una matrice di elementi e la scomposizione dei batch avviene su ogni riga.</span><span class="sxs-lookup"><span data-stu-id="12b60-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="12b60-141">Ambiti</span><span class="sxs-lookup"><span data-stu-id="12b60-141">Scopes</span></span>

<span data-ttu-id="12b60-142">È possibile toogroup una serie di azioni tra loro tramite un ambito.</span><span class="sxs-lookup"><span data-stu-id="12b60-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="12b60-143">Ciò è particolarmente utile per implementare la gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="12b60-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="12b60-144">Nella finestra di progettazione hello è possibile aggiungere un nuovo ambito e iniziare ad aggiungere le azioni all'interno.</span><span class="sxs-lookup"><span data-stu-id="12b60-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="12b60-145">È possibile definire gli ambiti nella visualizzazione di codice hello seguente:</span><span class="sxs-lookup"><span data-stu-id="12b60-145">You can define scopes in code-view like hello following:</span></span>


```
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