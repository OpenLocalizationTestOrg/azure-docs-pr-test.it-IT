---
title: Creare cicli e ambiti o suddividere i dati nei flussi di lavoro - App per la logica di Azure | Documenti di Microsoft
description: "Creare cicli per eseguire iterazioni sui dati, raggruppare le azioni in ambiti o suddividere i dati per avviare più flussi di lavoro logica nelle app per la logica di Azure."
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
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="c2add-103">Cicli, ambiti e debatching delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="c2add-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="c2add-104">Le app per la logica offrono una serie di metodi per usare matrici, raccolte, batch e cicli all'interno di un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c2add-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="c2add-105">Matrici e cicli ForEach</span><span class="sxs-lookup"><span data-stu-id="c2add-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="c2add-106">App per la logica consente di eseguire un ciclo su un set di dati e di eseguire un'azione per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="c2add-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="c2add-107">Per queste operazioni viene usata l'azione `foreach` .</span><span class="sxs-lookup"><span data-stu-id="c2add-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="c2add-108">Nella finestra di progettazione è possibile specificare l'aggiunta di un loop ForEach.</span><span class="sxs-lookup"><span data-stu-id="c2add-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="c2add-109">Dopo aver selezionato la matrice su cui si vuole eseguire un'iterazione, è possibile iniziare ad aggiungere azioni.</span><span class="sxs-lookup"><span data-stu-id="c2add-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="c2add-110">Attualmente è possibile eseguire solo un'azione per ogni loop ForEach, ma questa limitazione verrà rimossa nelle prossime settimane.</span><span class="sxs-lookup"><span data-stu-id="c2add-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="c2add-111">All'interno del loop è possibile iniziare a specificare cosa deve avvenire in corrispondenza di ogni valore della matrice.</span><span class="sxs-lookup"><span data-stu-id="c2add-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="c2add-112">Se si usa la visualizzazione del codice, è possibile specificare un loop ForEach come nell'illustrazione che segue.</span><span class="sxs-lookup"><span data-stu-id="c2add-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="c2add-113">In questo esempio di loop ForEach viene inviato un messaggio di posta elettronica per ogni indirizzo di posta elettronica che contiene "microsoft.com":</span><span class="sxs-lookup"><span data-stu-id="c2add-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="c2add-114">Un'azione `foreach` è in grado di eseguire l'iterazione su matrici con fino a 5.000 righe.</span><span class="sxs-lookup"><span data-stu-id="c2add-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="c2add-115">Per impostazione predefinita, ogni iterazione verrà eseguita in parallelo alle altre.</span><span class="sxs-lookup"><span data-stu-id="c2add-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="c2add-116">Cicli ForEach sequenziali</span><span class="sxs-lookup"><span data-stu-id="c2add-116">Sequential ForEach loops</span></span>

<span data-ttu-id="c2add-117">Per abilitare l'esecuzione sequenziale di un ciclo ForEach è necessario aggiungere l'opzione di operazione `Sequential`.</span><span class="sxs-lookup"><span data-stu-id="c2add-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="c2add-118">Ciclo Until</span><span class="sxs-lookup"><span data-stu-id="c2add-118">Until loop</span></span>
  
  <span data-ttu-id="c2add-119">È possibile eseguire un'azione o una serie di azioni finché non viene soddisfatta una condizione.</span><span class="sxs-lookup"><span data-stu-id="c2add-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="c2add-120">Lo scenario più comune è quello in cui si chiama un endpoint fino a ottenere la risposta desiderata.</span><span class="sxs-lookup"><span data-stu-id="c2add-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="c2add-121">Nella finestra di progettazione è possibile specificare l'aggiunta di un loop Until.</span><span class="sxs-lookup"><span data-stu-id="c2add-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="c2add-122">Dopo avere aggiunto le azioni nel loop, è possibile impostare la condizione di uscita, nonché i limiti del loop.</span><span class="sxs-lookup"><span data-stu-id="c2add-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="c2add-123">Si verifica un ritardo di 1 minuto tra i cicli del loop.</span><span class="sxs-lookup"><span data-stu-id="c2add-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="c2add-124">Se si usa la visualizzazione del codice, è possibile specificare un loop Until come nell'illustrazione che segue.</span><span class="sxs-lookup"><span data-stu-id="c2add-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="c2add-125">Questo è un esempio di chiamata a un endpoint HTTP finché nel corpo della risposta è presente il valore "Completed".</span><span class="sxs-lookup"><span data-stu-id="c2add-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="c2add-126">Ciò avviene in presenza di una di queste condizioni:</span><span class="sxs-lookup"><span data-stu-id="c2add-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="c2add-127">Lo stato della risposta HTTP è "Completed"</span><span class="sxs-lookup"><span data-stu-id="c2add-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="c2add-128">Sono stati fatti tentativi per 1 ora</span><span class="sxs-lookup"><span data-stu-id="c2add-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="c2add-129">Il ciclo è stato eseguito 100 volte</span><span class="sxs-lookup"><span data-stu-id="c2add-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="c2add-130">SplitOn e scomposizione batch</span><span class="sxs-lookup"><span data-stu-id="c2add-130">SplitOn and debatching</span></span>

<span data-ttu-id="c2add-131">In alcuni casi un trigger può ricevere una matrice di elementi che si preferisce separare per avviare un flusso di lavoro per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="c2add-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="c2add-132">Questa operazione può essere eseguita con il comando `spliton` .</span><span class="sxs-lookup"><span data-stu-id="c2add-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="c2add-133">Per impostazione predefinita, se lo swagger del trigger specifica un payload che è una matrice, viene aggiunto `spliton` e viene avviata un'esecuzione per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="c2add-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="c2add-134">SplitOn può essere aggiunto solo a un trigger.</span><span class="sxs-lookup"><span data-stu-id="c2add-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="c2add-135">L'operazione può essere configurata manualmente o sottoposta a override nella visualizzazione del codice di definizione.</span><span class="sxs-lookup"><span data-stu-id="c2add-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="c2add-136">Attualmente SplitOn è in grado di suddividere matrici con al massimo 5.000 elementi.</span><span class="sxs-lookup"><span data-stu-id="c2add-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="c2add-137">Non è possibile usare `spliton` e implementare anche il modello di risposta sincrona.</span><span class="sxs-lookup"><span data-stu-id="c2add-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="c2add-138">Qualsiasi flusso di lavoro chiamato che ha un'azione `response` oltre a `spliton` verrà eseguito in modo asincrono e invierà immediatamente una risposta `202 Accepted`.</span><span class="sxs-lookup"><span data-stu-id="c2add-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="c2add-139">SplitOn può essere specificato nella visualizzazione del codice, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="c2add-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="c2add-140">In questo caso viene ricevuta una matrice di elementi e la scomposizione dei batch avviene su ogni riga.</span><span class="sxs-lookup"><span data-stu-id="c2add-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="c2add-141">Ambiti</span><span class="sxs-lookup"><span data-stu-id="c2add-141">Scopes</span></span>

<span data-ttu-id="c2add-142">È possibile raggruppare una serie di azioni tra loro usando un ambito.</span><span class="sxs-lookup"><span data-stu-id="c2add-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="c2add-143">Ciò è particolarmente utile per implementare la gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="c2add-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="c2add-144">Nella finestra di progettazione è possibile aggiungere un nuovo ambito e iniziare ad aggiungere tutte le azioni all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="c2add-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="c2add-145">È possibile definire gli ambiti nella visualizzazione del codice come nell'esempio che segue:</span><span class="sxs-lookup"><span data-stu-id="c2add-145">You can define scopes in code-view like the following:</span></span>


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